# Kinesis Firehose Delivery Stream

Manage Kinesis Firehose Delivery Stream resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_kinesis_firehose_delivery_stream:
    extended_s3_stream:
      name: terraform-kinesis-firehose-extended-s3-test-stream
      destination: extended_s3
      extended_s3_configuration:
        role_arn: ${aws_iam_role.firehose_role.arn}
        bucket_arn: ${aws_s3_bucket.bucket.arn}
        processing_configuration:
          enabled: true
          processors:
            type: Lambda
            parameters:
              parameter_name: LambdaArn
              parameter_value: "${aws_lambda_function.lambda_processor.arn}:$LATEST"

resource:
  aws_s3_bucket:
    bucket:
      bucket: tf-test-bucket

resource:
  aws_s3_bucket_acl:
    bucket_acl:
      bucket: ${aws_s3_bucket.bucket.id}
      acl: private

data:
  aws_iam_policy_document:
    firehose_assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - firehose.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    firehose_role:
      name: firehose_test_role
      assume_role_policy: ${data.aws_iam_policy_document.firehose_assume_role.json}

data:
  aws_iam_policy_document:
    lambda_assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - lambda.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    lambda_iam:
      name: lambda_iam
      assume_role_policy: ${data.aws_iam_policy_document.lambda_assume_role.json}

resource:
  aws_lambda_function:
    lambda_processor:
      filename: lambda.zip
      function_name: firehose_lambda_processor
      role: ${aws_iam_role.lambda_iam.arn}
      handler: exports.handler
      runtime: nodejs20.x
```

## Extended S3 Destination with dynamic partitioning

```yaml
resource:
  aws_kinesis_firehose_delivery_stream:
    extended_s3_stream:
      name: terraform-kinesis-firehose-extended-s3-test-stream
      destination: extended_s3
      extended_s3_configuration:
        role_arn: ${aws_iam_role.firehose_role.arn}
        bucket_arn: ${aws_s3_bucket.bucket.arn}
        buffering_size: 64
        dynamic_partitioning_configuration:
          enabled: true
        prefix: "data/customer_id=!{partitionKeyFromQuery:customer_id}/year=!{timestamp:yyyy}/month=!{timestamp:MM}/day=!{timestamp:dd}/hour=!{timestamp:HH}/"
        error_output_prefix: "errors/year=!{timestamp:yyyy}/month=!{timestamp:MM}/day=!{timestamp:dd}/hour=!{timestamp:HH}/!{firehose:error-output-type}/"
        processing_configuration:
          enabled: true
          processors:
            type: RecordDeAggregation
            parameters:
              parameter_name: SubRecordType
              parameter_value: JSON
          processors:
            type: AppendDelimiterToRecord
          processors:
            type: MetadataExtraction
            parameters:
              parameter_name: JsonParsingEngine
              parameter_value: JQ-1.6
            parameters:
              parameter_name: MetadataExtractionQuery
              parameter_value: "{customer_id:.customer_id}"
```

## Redshift Destination

```yaml
resource:
  aws_redshift_cluster:
    test_cluster:
      cluster_identifier: tf-redshift-cluster
      database_name: test
      master_username: testuser
      master_password: T3stPass
      node_type: dc1.large
      cluster_type: single-node

resource:
  aws_kinesis_firehose_delivery_stream:
    test_stream:
      name: terraform-kinesis-firehose-test-stream
      destination: redshift
      redshift_configuration:
        role_arn: ${aws_iam_role.firehose_role.arn}
        cluster_jdbcurl: "jdbc:redshift://${aws_redshift_cluster.test_cluster.endpoint}/${aws_redshift_cluster.test_cluster.database_name}"
        username: testuser
        password: T3stPass
        data_table_name: test-table
        copy_options: "delimiter '|'" # the default delimiter
        data_table_columns: test-col
        s3_backup_mode: Enabled
        s3_configuration:
          role_arn: ${aws_iam_role.firehose_role.arn}
          bucket_arn: ${aws_s3_bucket.bucket.arn}
          buffering_size: 10
          buffering_interval: 400
          compression_format: GZIP
        s3_backup_configuration:
          role_arn: ${aws_iam_role.firehose_role.arn}
          bucket_arn: ${aws_s3_bucket.bucket.arn}
          buffering_size: 15
          buffering_interval: 300
          compression_format: GZIP
```

## Elasticsearch Destination

```yaml
resource:
  aws_elasticsearch_domain:
    test_cluster:
      domain_name: firehose-es-test

resource:
  aws_kinesis_firehose_delivery_stream:
    test_stream:
      name: terraform-kinesis-firehose-test-stream
      destination: elasticsearch
      elasticsearch_configuration:
        domain_arn: ${aws_elasticsearch_domain.test_cluster.arn}
        role_arn: ${aws_iam_role.firehose_role.arn}
        index_name: test
        type_name: test
        s3_configuration:
          role_arn: ${aws_iam_role.firehose_role.arn}
          bucket_arn: ${aws_s3_bucket.bucket.arn}
          buffering_size: 10
          buffering_interval: 400
          compression_format: GZIP
        processing_configuration:
          enabled: true
          processors:
            type: Lambda
            parameters:
              parameter_name: LambdaArn
              parameter_value: "${aws_lambda_function.lambda_processor.arn}:$LATEST"
```

## Elasticsearch Destination With VPC

```yaml
resource:
  aws_elasticsearch_domain:
    test_cluster:
      domain_name: es-test
      cluster_config:
        instance_count: 2
        zone_awareness_enabled: true
        instance_type: t2.small.elasticsearch
      ebs_options:
        ebs_enabled: true
        volume_size: 10
      vpc_options:
        security_group_ids: 
          - ${aws_security_group.first.id}
        subnet_ids: 
          - ${aws_subnet.first.id}
          - ${aws_subnet.second.id}

data:
  aws_iam_policy_document:
    firehose-elasticsearch:
      statement:
        effect: Allow
        actions: 
          - "es:*"
        resources:
          - ${aws_elasticsearch_domain.test_cluster.arn}
          - "${aws_elasticsearch_domain.test_cluster.arn}/*"
      statement:
        effect: Allow
        actions:
          - "ec2:DescribeVpcs"
          - "ec2:DescribeVpcAttribute"
          - "ec2:DescribeSubnets"
          - "ec2:DescribeSecurityGroups"
          - "ec2:DescribeNetworkInterfaces"
          - "ec2:CreateNetworkInterface"
          - "ec2:CreateNetworkInterfacePermission"
          - "ec2:DeleteNetworkInterface"
        resources: 
          - "*"

resource:
  aws_iam_role_policy:
    firehose-elasticsearch:
      name: elasticsearch
      role: ${aws_iam_role.firehose.id}
      policy: ${data.aws_iam_policy_document.firehose-elasticsearch.json}

resource:
  aws_kinesis_firehose_delivery_stream:
    test:
      depends_on: 
        - ${aws_iam_role_policy.firehose-elasticsearch}
      name: terraform-kinesis-firehose-es
      destination: elasticsearch
      elasticsearch_configuration:
        domain_arn: ${aws_elasticsearch_domain.test_cluster.arn}
        role_arn: ${aws_iam_role.firehose.arn}
        index_name: test
        type_name: test
        s3_configuration:
          role_arn: ${aws_iam_role.firehose.arn}
          bucket_arn: ${aws_s3_bucket.bucket.arn}
        vpc_config:
          subnet_ids: 
            - ${aws_subnet.first.id}
            - ${aws_subnet.second.id}
          security_group_ids: 
            - ${aws_security_group.first.id}
          role_arn: ${aws_iam_role.firehose.arn}
```

## OpenSearch Destination

```yaml
resource:
  aws_opensearch_domain:
    test_cluster:
      domain_name: firehose-os-test

resource:
  aws_kinesis_firehose_delivery_stream:
    test_stream:
      name: terraform-kinesis-firehose-test-stream
      destination: opensearch
      opensearch_configuration:
        domain_arn: ${aws_opensearch_domain.test_cluster.arn}
        role_arn: ${aws_iam_role.firehose_role.arn}
        index_name: test
        s3_configuration:
          role_arn: ${aws_iam_role.firehose_role.arn}
          bucket_arn: ${aws_s3_bucket.bucket.arn}
          buffering_size: 10
          buffering_interval: 400
          compression_format: GZIP
        processing_configuration:
          enabled: true
          processors:
            type: Lambda
            parameters:
              parameter_name: LambdaArn
              parameter_value: "${aws_lambda_function.lambda_processor.arn}:$LATEST"
```

## OpenSearch Destination With VPC

```yaml
resource:
  aws_opensearch_domain:
    test_cluster:
      domain_name: es-test
      cluster_config:
        instance_count: 2
        zone_awareness_enabled: true
        instance_type: m4.large.search
      ebs_options:
        ebs_enabled: true
        volume_size: 10
      vpc_options:
        security_group_ids: 
          - ${aws_security_group.first.id}
        subnet_ids: 
          - ${aws_subnet.first.id}
          - ${aws_subnet.second.id}

resource:
  aws_iam_role_policy:
    firehose-opensearch:
      name: opensearch
      role: ${aws_iam_role.firehose.id}
      policy: |
        {
        "Version": "2012-10-17",
        "Statement": [
        {
        "Effect": "Allow",
        "Action": [
        "es:*"
        ],
        "Resource": [
        "${aws_opensearch_domain.test_cluster.arn}",
        "${aws_opensearch_domain.test_cluster.arn}/*"
        ]
        },
        {
        "Effect": "Allow",
        "Action": [
        "ec2:DescribeVpcs",
        "ec2:DescribeVpcAttribute",
        "ec2:DescribeSubnets",
        "ec2:DescribeSecurityGroups",
        "ec2:DescribeNetworkInterfaces",
        "ec2:CreateNetworkInterface",
        "ec2:CreateNetworkInterfacePermission",
        "ec2:DeleteNetworkInterface"
        ],
        "Resource": [
        "*"
        ]
        }
        ]
        }

resource:
  aws_kinesis_firehose_delivery_stream:
    test:
      depends_on: 
        - ${aws_iam_role_policy.firehose-opensearch}
      name: terraform-kinesis-firehose-os
      destination: opensearch
      opensearch_configuration:
        domain_arn: ${aws_opensearch_domain.test_cluster.arn}
        role_arn: ${aws_iam_role.firehose.arn}
        index_name: test
        s3_configuration:
          role_arn: ${aws_iam_role.firehose.arn}
          bucket_arn: ${aws_s3_bucket.bucket.arn}
        vpc_config:
          subnet_ids: 
            - ${aws_subnet.first.id}
            - ${aws_subnet.second.id}
          security_group_ids: 
            - ${aws_security_group.first.id}
          role_arn: ${aws_iam_role.firehose.arn}
```

## OpenSearch Serverless Destination

```yaml
resource:
  aws_opensearchserverless_collection:
    test_collection:
      name: firehose-osserverless-test

resource:
  aws_kinesis_firehose_delivery_stream:
    test_stream:
      name: terraform-kinesis-firehose-test-stream
      destination: opensearchserverless
      opensearchserverless_configuration:
        collection_endpoint: ${aws_opensearchserverless_collection.test_collection.collection_endpoint}
        role_arn: ${aws_iam_role.firehose_role.arn}
        index_name: test
        s3_configuration:
          role_arn: ${aws_iam_role.firehose_role.arn}
          bucket_arn: ${aws_s3_bucket.bucket.arn}
          buffering_size: 10
          buffering_interval: 400
          compression_format: GZIP
        processing_configuration:
          enabled: true
          processors:
            type: Lambda
            parameters:
              parameter_name: LambdaArn
              parameter_value: "${aws_lambda_function.lambda_processor.arn}:$LATEST"
```

## Iceberg Destination

```yaml
data:
  aws_caller_identity:
    current:

data:
  aws_partition:
    current:

data:
  aws_region:
    current:

resource:
  aws_s3_bucket:
    bucket:
      bucket: test-bucket
      force_destroy: true

resource:
  aws_glue_catalog_database:
    test:
      name: test

resource:
  aws_glue_catalog_table:
    test:
      name: test
      database_name: ${aws_glue_catalog_database.test.name}
      parameters:
        format: parquet
      table_type: EXTERNAL_TABLE
      open_table_format_input:
        iceberg_input:
          metadata_operation: CREATE
          version: 2
      storage_descriptor:
        location: "s3://${aws_s3_bucket.bucket.id}"
        columns:
          name: my_column_1
          type: int

resource:
  aws_kinesis_firehose_delivery_stream:
    test_stream:
      name: terraform-kinesis-firehose-test-stream
      destination: iceberg
      iceberg_configuration:
        role_arn: ${aws_iam_role.firehose_role.arn}
        catalog_arn: "arn:${data.aws_partition.current.partition}:glue:${data.aws_region.current.region}:${data.aws_caller_identity.current.account_id}:catalog"
        buffering_size: 10
        buffering_interval: 400
        s3_configuration:
          role_arn: ${aws_iam_role.firehose_role.arn}
          bucket_arn: ${aws_s3_bucket.bucket.arn}
        destination_table_configuration:
          database_name: ${aws_glue_catalog_database.test.name}
          table_name: ${aws_glue_catalog_table.test.name}
        processing_configuration:
          enabled: true
          processors:
            type: Lambda
            parameters:
              parameter_name: LambdaArn
              parameter_value: "${aws_lambda_function.lambda_processor.arn}:$LATEST"
```

## Splunk Destination

```yaml
resource:
  aws_kinesis_firehose_delivery_stream:
    test_stream:
      name: terraform-kinesis-firehose-test-stream
      destination: splunk
      splunk_configuration:
        hec_endpoint: "https://http-inputs-mydomain.splunkcloud.com:443"
        hec_token: 51D4DA16-C61B-4F5F-8EC7-ED4301342A4A
        hec_acknowledgment_timeout: 600
        hec_endpoint_type: Event
        s3_backup_mode: FailedEventsOnly
        s3_configuration:
          role_arn: ${aws_iam_role.firehose.arn}
          bucket_arn: ${aws_s3_bucket.bucket.arn}
          buffering_size: 10
          buffering_interval: 400
          compression_format: GZIP
```

## HTTP Endpoint (e.g., New Relic) Destination

```yaml
resource:
  aws_kinesis_firehose_delivery_stream:
    test_stream:
      name: terraform-kinesis-firehose-test-stream
      destination: http_endpoint
      http_endpoint_configuration:
        url: "https://aws-api.newrelic.com/firehose/v1"
        name: New Relic
        access_key: my-key
        buffering_size: 15
        buffering_interval: 600
        role_arn: ${aws_iam_role.firehose.arn}
        s3_backup_mode: FailedDataOnly
        s3_configuration:
          role_arn: ${aws_iam_role.firehose.arn}
          bucket_arn: ${aws_s3_bucket.bucket.arn}
          buffering_size: 10
          buffering_interval: 400
          compression_format: GZIP
        request_configuration:
          content_encoding: GZIP
          common_attributes:
            name: testname
            value: testvalue
          common_attributes:
            name: testname2
            value: testvalue2
```

## Snowflake Destination

```yaml
resource:
  aws_kinesis_firehose_delivery_stream:
    example_snowflake_destination:
      name: example-snowflake-destination
      destination: snowflake
      snowflake_configuration:
        account_url: "https://example.snowflakecomputing.com"
        buffering_size: 15
        buffering_interval: 600
        database: example-db
        private_key: ...
        role_arn: ${aws_iam_role.firehose.arn}
        schema: example-schema
        table: example-table
        user: example-usr
        s3_configuration:
          role_arn: ${aws_iam_role.firehose.arn}
          bucket_arn: ${aws_s3_bucket.bucket.arn}
          buffering_size: 10
          buffering_interval: 400
          compression_format: GZIP
```
