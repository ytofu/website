# Flow Log

Manage Flow Log resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_flow_log:
    example:
      iam_role_arn: ${aws_iam_role.example.arn}
      log_destination: ${aws_cloudwatch_log_group.example.arn}
      traffic_type: ALL
      vpc_id: ${aws_vpc.example.id}

resource:
  aws_cloudwatch_log_group:
    example:
      name: example

data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - vpc-flow-logs.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    example:
      name: example
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

data:
  aws_iam_policy_document:
    example:
      statement:
        effect: Allow
        actions:
          - "logs:CreateLogGroup"
          - "logs:CreateLogStream"
          - "logs:PutLogEvents"
          - "logs:DescribeLogGroups"
          - "logs:DescribeLogStreams"
        resources: 
          - "*"

resource:
  aws_iam_role_policy:
    example:
      name: example
      role: ${aws_iam_role.example.id}
      policy: ${data.aws_iam_policy_document.example.json}
```

## Amazon Data Firehose logging

```yaml
resource:
  aws_flow_log:
    example:
      log_destination: ${aws_kinesis_firehose_delivery_stream.example.arn}
      log_destination_type: kinesis-data-firehose
      traffic_type: ALL
      vpc_id: ${aws_vpc.example.id}

resource:
  aws_kinesis_firehose_delivery_stream:
    example:
      name: kinesis_firehose_test
      destination: extended_s3
      extended_s3_configuration:
        role_arn: ${aws_iam_role.example.arn}
        bucket_arn: ${aws_s3_bucket.example.arn}
      tags: 

resource:
  aws_s3_bucket:
    example:
      bucket: example

resource:
  aws_s3_bucket_acl:
    example:
      bucket: ${aws_s3_bucket.example.id}
      acl: private

data:
  aws_iam_policy_document:
    assume_role:
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
    example:
      name: firehose_test_role
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

data:
  aws_iam_policy_document:
    example:
      effect: Allow
      actions:
        - "logs:CreateLogDelivery"
        - "logs:DeleteLogDelivery"
        - "logs:ListLogDeliveries"
        - "logs:GetLogDelivery"
        - "firehose:TagDeliveryStream"
      resources: 
        - "*"

resource:
  aws_iam_role_policy:
    example:
      name: test
      role: ${aws_iam_role.example.id}
      policy: ${data.aws_iam_policy_document.example.json}
```

## S3 Logging

```yaml
resource:
  aws_flow_log:
    example:
      log_destination: ${aws_s3_bucket.example.arn}
      log_destination_type: s3
      traffic_type: ALL
      vpc_id: ${aws_vpc.example.id}

resource:
  aws_s3_bucket:
    example:
      bucket: example
```

## S3 Logging in Apache Parquet format with per-hour partitions

```yaml
resource:
  aws_flow_log:
    example:
      log_destination: ${aws_s3_bucket.example.arn}
      log_destination_type: s3
      traffic_type: ALL
      vpc_id: ${aws_vpc.example.id}
      destination_options:
        file_format: parquet
        per_hour_partition: true

resource:
  aws_s3_bucket:
    example:
      bucket: example
```

## Cross-Account Amazon Data Firehose Logging

```yaml
resource:
  aws_vpc:
    src:

data:
  aws_iam_policy_document:
    src_assume_role_policy:
      statement:
        actions: 
          - "sts:AssumeRole"
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - delivery.logs.amazonaws.com

resource:
  aws_iam_role:
    src:
      name: tf-example-mySourceRole
      assume_role_policy: ${data.aws_iam_policy_document.src_assume_role_policy.json}

data:
  aws_iam_policy_document:
    src_role_policy:
      statement:
        effect: Allow
        actions: 
          - "iam:PassRole"
        resources: 
          - ${aws_iam_role.src.arn}
        condition:
          test: StringEquals
          values: 
            - delivery.logs.amazonaws.com
        condition:
          test: StringLike
          values: 
            - ${aws_vpc.src.arn}
      statement:
        effect: Allow
        actions:
          - "logs:CreateLogDelivery"
          - "logs:DeleteLogDelivery"
          - "logs:ListLogDeliveries"
          - "logs:GetLogDelivery"
        resources: 
          - "*"
      statement:
        effect: Allow
        actions: 
          - "sts:AssumeRole"
        resources: 
          - ${aws_iam_role.dst.arn}

resource:
  aws_iam_role_policy:
    src_policy:
      name: tf-example-mySourceRolePolicy
      role: ${aws_iam_role.src.name}
      policy: ${data.aws_iam_policy_document.src_role_policy.json}

resource:
  aws_flow_log:
    src:
      log_destination_type: kinesis-data-firehose
      log_destination: ${aws_kinesis_firehose_delivery_stream.dst.arn}
      traffic_type: ALL
      vpc_id: ${aws_vpc.src.id}
      iam_role_arn: ${aws_iam_role.src.arn}
      deliver_cross_account_role: ${aws_iam_role.dst.arn}

data:
  aws_iam_policy_document:
    dst_assume_role_policy:
      statement:
        actions: 
          - "sts:AssumeRole"
        effect: Allow
        principals:
          type: AWS
          identifiers: 
            - ${aws_iam_role.src.arn}

resource:
  aws_iam_role:
    dst:
      name: "AWSLogDeliveryFirehoseCrossAccountRole" # must start with "AWSLogDeliveryFirehoseCrossAccountRolePolicy"
      assume_role_policy: ${data.aws_iam_policy_document.dst_assume_role_policy.json}

data:
  aws_iam_policy_document:
    dst_role_policy:
      statement:
        effect: Allow
        actions:
          - "iam:CreateServiceLinkedRole"
          - "firehose:TagDeliveryStream"
        resources: 
          - "*"

resource:
  aws_iam_role_policy:
    dst:
      name: AWSLogDeliveryFirehoseCrossAccountRolePolicy
      role: ${aws_iam_role.dst.name}
      policy: ${data.aws_iam_policy_document.dst_role_policy.json}

resource:
  aws_kinesis_firehose_delivery_stream:
    dst:
      tags:
        LogDeliveryEnabled: true
```
