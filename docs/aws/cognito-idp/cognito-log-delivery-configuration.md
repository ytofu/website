# Cognito Log Delivery Configuration

Manage Cognito Log Delivery Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cognito_user_pool:
    example:
      name: example

resource:
  aws_cloudwatch_log_group:
    example:
      name: example

resource:
  aws_cognito_log_delivery_configuration:
    example:
      user_pool_id: ${aws_cognito_user_pool.example.id}
      log_configurations:
        event_source: userNotification
        log_level: ERROR
        cloud_watch_logs_configuration:
          log_group_arn: ${aws_cloudwatch_log_group.example.arn}
```

## Multiple Log Configurations with Different Destinations

```yaml
resource:
  aws_cognito_user_pool:
    example:
      name: example

resource:
  aws_cloudwatch_log_group:
    example:
      name: example

resource:
  aws_s3_bucket:
    example:
      bucket: example-bucket
      force_destroy: true

resource:
  aws_iam_role:
    firehose:
      name: firehose-role
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": "sts:AssumeRole" "Effect": "Allow" "Principal": { "Service": "firehose.amazonaws.com" } } ] }'

resource:
  aws_iam_role_policy:
    firehose:
      name: firehose-policy
      role: ${aws_iam_role.firehose.id}
      policy: '{ "Version": "2012-10-17" "Statement": [ { "Effect": "Allow" "Action": [ "s3:AbortMultipartUpload", "s3:GetBucketLocation", "s3:GetObject", "s3:ListBucket", "s3:ListBucketMultipartUploads", "s3:PutObject" ] "Resource": [ aws_s3_bucket.example.arn, "${aws_s3_bucket.example.arn}/*" ] } ] }'

resource:
  aws_kinesis_firehose_delivery_stream:
    example:
      name: example-stream
      destination: extended_s3
      extended_s3_configuration:
        role_arn: ${aws_iam_role.firehose.arn}
        bucket_arn: ${aws_s3_bucket.example.arn}

resource:
  aws_cognito_log_delivery_configuration:
    example:
      user_pool_id: ${aws_cognito_user_pool.example.id}
      log_configurations:
        event_source: userNotification
        log_level: INFO
        cloud_watch_logs_configuration:
          log_group_arn: ${aws_cloudwatch_log_group.example.arn}
      log_configurations:
        event_source: userAuthEvents
        log_level: ERROR
        firehose_configuration:
          stream_arn: ${aws_kinesis_firehose_delivery_stream.example.arn}
```

## S3 Configuration

```yaml
resource:
  aws_cognito_user_pool:
    example:
      name: example

resource:
  aws_s3_bucket:
    example:
      bucket: example-bucket
      force_destroy: true

resource:
  aws_cognito_log_delivery_configuration:
    example:
      user_pool_id: ${aws_cognito_user_pool.example.id}
      log_configurations:
        event_source: userNotification
        log_level: ERROR
        s3_configuration:
          bucket_arn: ${aws_s3_bucket.example.arn}
```
