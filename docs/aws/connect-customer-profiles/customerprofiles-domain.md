# Customerprofiles Domain

Manage Customerprofiles Domain resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_customerprofiles_domain:
    example:
      domain_name: example
```

## With SQS DLQ and KMS set

```yaml
resource:
  aws_sqs_queue:
    example:
      name: example
      policy: '{ "Version": "2012-10-17" "Statement": [ { "Sid": "Customer Profiles SQS policy" "Effect": "Allow" "Action": [ "sqs:SendMessage", ], "Resource": "*" "Principal": { "Service": "profile.amazonaws.com" } }, ] }'

resource:
  aws_kms_key:
    example:
      description: example
      deletion_window_in_days: 10

resource:
  aws_s3_bucket:
    example:
      bucket: example
      force_destroy: true

resource:
  aws_s3_bucket_policy:
    example:
      bucket: ${aws_s3_bucket.example.id}
      policy: '{ "Version": "2012-10-17" "Statement": [ { "Sid": "Customer Profiles S3 policy" "Effect": "Allow" "Action": [ "s3:GetObject", "s3:PutObject", "s3:ListBucket", ] "Resource": [ aws_s3_bucket.example.arn, "${aws_s3_bucket.example.arn}/*", ] "Principal": { "Service": "profile.amazonaws.com" } }, ] }'

resource:
  aws_customerprofiles_domain:
    test:
      domain_name: example
      dead_letter_queue_url: ${aws_sqs_queue.example.id}
      default_encryption_key: ${aws_kms_key.example.arn}
      default_expiration_days: 365
```
