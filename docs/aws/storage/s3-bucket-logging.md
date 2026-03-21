# S3 Bucket Logging

Manage S3 Bucket Logging resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_s3_bucket:
    logging:
      bucket: access-logging-bucket

data:
  aws_iam_policy_document:
    logging_bucket_policy:
      statement:
        principals:
          identifiers: 
            - logging.s3.amazonaws.com
          type: Service
        actions: 
          - "s3:PutObject"
        resources: 
          - "${aws_s3_bucket.logging.arn}/*"
        condition:
          test: StringEquals
          values: 
            - ${data.aws_caller_identity.current.account_id}

resource:
  aws_s3_bucket_policy:
    logging:
      bucket: ${aws_s3_bucket.logging.bucket}
      policy: ${data.aws_iam_policy_document.logging_bucket_policy.json}

resource:
  aws_s3_bucket:
    example:
      bucket: example-bucket

resource:
  aws_s3_bucket_logging:
    example:
      bucket: ${aws_s3_bucket.example.bucket}
      target_bucket: ${aws_s3_bucket.logging.bucket}
      target_prefix: log/
      target_object_key_format:
        partitioned_prefix:
          partition_date_source: EventTime
```

## Grant permission by using bucket ACL

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: my-tf-example-bucket

resource:
  aws_s3_bucket_acl:
    example:
      bucket: ${aws_s3_bucket.example.id}
      acl: private

resource:
  aws_s3_bucket:
    log_bucket:
      bucket: my-tf-log-bucket

resource:
  aws_s3_bucket_acl:
    log_bucket_acl:
      bucket: ${aws_s3_bucket.log_bucket.id}
      acl: log-delivery-write

resource:
  aws_s3_bucket_logging:
    example:
      bucket: ${aws_s3_bucket.example.id}
      target_bucket: ${aws_s3_bucket.log_bucket.id}
      target_prefix: log/
```
