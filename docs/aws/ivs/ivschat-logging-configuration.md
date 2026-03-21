# Ivschat Logging Configuration

Manage Ivschat Logging Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudwatch_log_group:
    example:

resource:
  aws_ivschat_logging_configuration:
    example:
      destination_configuration:
        cloudwatch_logs:
          log_group_name: ${aws_cloudwatch_log_group.example.name}
```

## Basic Usage - Logging to Kinesis Firehose with Extended S3

```yaml
resource:
  aws_kinesis_firehose_delivery_stream:
    example:
      name: terraform-kinesis-firehose-extended-s3-example-stream
      destination: extended_s3
      extended_s3_configuration:
        role_arn: ${aws_iam_role.example.arn}
        bucket_arn: ${aws_s3_bucket.example.arn}
      tags: 

resource:
  aws_s3_bucket:
    example:
      bucket_prefix: tf-ivschat-logging-bucket

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
      name: firehose_example_role
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

resource:
  aws_ivschat_logging_configuration:
    example:
      destination_configuration:
        firehose:
          delivery_stream_name: ${aws_kinesis_firehose_delivery_stream.example.name}
```

## Basic Usage - Logging to S3

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket_name: tf-ivschat-logging
      force_destroy: true

resource:
  aws_ivschat_logging_configuration:
    example:
      destination_configuration:
        s3:
          bucket_name: ${aws_s3_bucket.example.id}
```
