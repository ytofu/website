# Cloudwatch Metric Stream

Manage Cloudwatch Metric Stream resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudwatch_metric_stream:
    main:
      name: my-metric-stream
      role_arn: ${aws_iam_role.metric_stream_to_firehose.arn}
      firehose_arn: ${aws_kinesis_firehose_delivery_stream.s3_stream.arn}
      output_format: json
      include_filter:
        namespace: AWS/EC2
        metric_names: 
          - CPUUtilization
          - NetworkOut
      include_filter:
        namespace: AWS/EBS
        metric_names: []

data:
  aws_iam_policy_document:
    streams_assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - streams.metrics.cloudwatch.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    metric_stream_to_firehose:
      name: metric_stream_to_firehose_role
      assume_role_policy: ${data.aws_iam_policy_document.streams_assume_role.json}

data:
  aws_iam_policy_document:
    metric_stream_to_firehose:
      statement:
        effect: Allow
        actions:
          - "firehose:PutRecord"
          - "firehose:PutRecordBatch"
        resources: 
          - ${aws_kinesis_firehose_delivery_stream.s3_stream.arn}

resource:
  aws_iam_role_policy:
    metric_stream_to_firehose:
      name: default
      role: ${aws_iam_role.metric_stream_to_firehose.id}
      policy: ${data.aws_iam_policy_document.metric_stream_to_firehose.json}

resource:
  aws_s3_bucket:
    bucket:
      bucket: metric-stream-test-bucket

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
    firehose_to_s3:
      assume_role_policy: ${data.aws_iam_policy_document.firehose_assume_role.json}

data:
  aws_iam_policy_document:
    firehose_to_s3:
      statement:
        effect: Allow
        actions:
          - "s3:AbortMultipartUpload"
          - "s3:GetBucketLocation"
          - "s3:GetObject"
          - "s3:ListBucket"
          - "s3:ListBucketMultipartUploads"
          - "s3:PutObject"
        resources:
          - ${aws_s3_bucket.bucket.arn}
          - "${aws_s3_bucket.bucket.arn}/*"

resource:
  aws_iam_role_policy:
    firehose_to_s3:
      name: default
      role: ${aws_iam_role.firehose_to_s3.id}
      policy: ${data.aws_iam_policy_document.firehose_to_s3.json}

resource:
  aws_kinesis_firehose_delivery_stream:
    s3_stream:
      name: metric-stream-test-stream
      destination: extended_s3
      extended_s3_configuration:
        role_arn: ${aws_iam_role.firehose_to_s3.arn}
        bucket_arn: ${aws_s3_bucket.bucket.arn}
```

## Additional Statistics

```yaml
resource:
  aws_cloudwatch_metric_stream:
    main:
      name: my-metric-stream
      role_arn: ${aws_iam_role.metric_stream_to_firehose.arn}
      firehose_arn: ${aws_kinesis_firehose_delivery_stream.s3_stream.arn}
      output_format: json
      statistics_configuration:
        additional_statistics:
          - p1
          - tm99
        include_metric:
          metric_name: CPUUtilization
          namespace: AWS/EC2
      statistics_configuration:
        additional_statistics:
          - "TS(50.5:)"
        include_metric:
          metric_name: CPUUtilization
          namespace: AWS/EC2
```
