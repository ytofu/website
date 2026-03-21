# S3 Bucket Object

Manage S3 Bucket Object resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket_object:
    object:
      bucket: your_bucket_name
      key: new_object_key
      source: path/to/file
      etag: ${filemd5("path/to/file")}
```

## Encrypting with KMS Key

```yaml
resource:
  aws_kms_key:
    examplekms:
      description: KMS key 1
      deletion_window_in_days: 7

resource:
  aws_s3_bucket:
    examplebucket:
      bucket: examplebuckettftest

resource:
  aws_s3_bucket_acl:
    example:
      bucket: ${aws_s3_bucket.examplebucket.id}
      acl: private

resource:
  aws_s3_bucket_object:
    example:
      key: someobject
      bucket: ${aws_s3_bucket.examplebucket.id}
      source: index.html
      kms_key_id: ${aws_kms_key.examplekms.arn}
```

## Server Side Encryption with S3 Default Master Key

```yaml
resource:
  aws_s3_bucket:
    examplebucket:
      bucket: examplebuckettftest

resource:
  aws_s3_bucket_acl:
    example:
      bucket: ${aws_s3_bucket.examplebucket.id}
      acl: private

resource:
  aws_s3_bucket_object:
    example:
      key: someobject
      bucket: ${aws_s3_bucket.examplebucket.id}
      source: index.html
      server_side_encryption: "aws:kms"
```

## Server Side Encryption with AWS-Managed Key

```yaml
resource:
  aws_s3_bucket:
    examplebucket:
      bucket: examplebuckettftest

resource:
  aws_s3_bucket_acl:
    example:
      bucket: ${aws_s3_bucket.examplebucket.id}
      acl: private

resource:
  aws_s3_bucket_object:
    example:
      key: someobject
      bucket: ${aws_s3_bucket.examplebucket.id}
      source: index.html
      server_side_encryption: AES256
```

## S3 Object Lock

```yaml
resource:
  aws_s3_bucket:
    examplebucket:
      bucket: examplebuckettftest
      object_lock_enabled: true

resource:
  aws_s3_bucket_acl:
    example:
      bucket: ${aws_s3_bucket.examplebucket.id}
      acl: private

resource:
  aws_s3_bucket_versioning:
    example:
      bucket: ${aws_s3_bucket.examplebucket.id}
      versioning_configuration:
        status: Enabled

resource:
  aws_s3_bucket_object:
    example:
      depends_on: 
        - ${aws_s3_bucket_versioning.example}
      key: someobject
      bucket: ${aws_s3_bucket.examplebucket.id}
      source: important.txt
      object_lock_legal_hold_status: ON
      object_lock_mode: GOVERNANCE
      object_lock_retain_until_date: "2021-12-31T23:59:60Z"
      force_destroy: true
```
