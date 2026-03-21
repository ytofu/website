# S3 Bucket Replication Configuration

Configure cross-region replication for S3 buckets using ytofu YAML.

## Basic Replication

```yaml
resource:
  aws_iam_role:
    replication:
      name: tf-iam-role-replication
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

  aws_iam_policy:
    replication:
      name: tf-iam-role-policy-replication
      policy: ${data.aws_iam_policy_document.replication.json}

  aws_iam_role_policy_attachment:
    replication:
      role: ${aws_iam_role.replication.name}
      policy_arn: ${aws_iam_policy.replication.arn}

  aws_s3_bucket:
    source:
      bucket: source-bucket

    destination:
      bucket: destination-bucket
      provider: aws.central

  aws_s3_bucket_versioning:
    source:
      bucket: ${aws_s3_bucket.source.id}
      versioning_configuration:
        status: Enabled

    destination:
      bucket: ${aws_s3_bucket.destination.id}
      versioning_configuration:
        status: Enabled
      provider: aws.central

  aws_s3_bucket_replication_configuration:
    replication:
      role: ${aws_iam_role.replication.arn}
      bucket: ${aws_s3_bucket.source.id}
      depends_on:
        - aws_s3_bucket_versioning.source
      rule:
        - id: replicate-all
          status: Enabled
          destination:
            bucket: ${aws_s3_bucket.destination.arn}
            storage_class: STANDARD
```

## With Prefix Filter

```yaml
resource:
  aws_s3_bucket_replication_configuration:
    replication:
      role: ${aws_iam_role.replication.arn}
      bucket: ${aws_s3_bucket.source.id}
      rule:
        - id: replicate-logs
          status: Enabled
          filter:
            prefix: logs/
          destination:
            bucket: ${aws_s3_bucket.destination.arn}
```

## With SSE-KMS Encryption

```yaml
resource:
  aws_s3_bucket_replication_configuration:
    replication:
      role: ${aws_iam_role.replication.arn}
      bucket: ${aws_s3_bucket.source.id}
      rule:
        - id: replicate-encrypted
          status: Enabled
          source_selection_criteria:
            sse_kms_encrypted_objects:
              status: Enabled
          destination:
            bucket: ${aws_s3_bucket.destination.arn}
            encryption_configuration:
              replica_kms_key_id: ${aws_kms_key.dest.arn}
```
