# S3 Bucket Versioning

Manage S3 Bucket Versioning resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: example-bucket

resource:
  aws_s3_bucket_acl:
    example:
      bucket: ${aws_s3_bucket.example.id}
      acl: private

resource:
  aws_s3_bucket_versioning:
    versioning_example:
      bucket: ${aws_s3_bucket.example.id}
      versioning_configuration:
        status: Enabled
```

## With Versioning Disabled

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: example-bucket

resource:
  aws_s3_bucket_acl:
    example:
      bucket: ${aws_s3_bucket.example.id}
      acl: private

resource:
  aws_s3_bucket_versioning:
    versioning_example:
      bucket: ${aws_s3_bucket.example.id}
      versioning_configuration:
        status: Disabled
```

## Object Dependency On Versioning

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: yotto

resource:
  aws_s3_bucket_versioning:
    example:
      bucket: ${aws_s3_bucket.example.id}
      versioning_configuration:
        status: Enabled

resource:
  aws_s3_object:
    example:
      bucket: ${aws_s3_bucket_versioning.example.id}
      key: droeloe
      source: example.txt
```
