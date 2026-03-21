# S3 Bucket Ownership Controls

Configure object ownership settings for S3 buckets using ytofu YAML.

## BucketOwnerPreferred

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: my-tf-example-bucket

  aws_s3_bucket_ownership_controls:
    example:
      bucket: ${aws_s3_bucket.example.id}
      rule:
        object_ownership: BucketOwnerPreferred
```

## BucketOwnerEnforced (Disable ACLs)

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: my-tf-example-bucket

  aws_s3_bucket_ownership_controls:
    example:
      bucket: ${aws_s3_bucket.example.id}
      rule:
        object_ownership: BucketOwnerEnforced
```

## ObjectWriter

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: my-tf-example-bucket

  aws_s3_bucket_ownership_controls:
    example:
      bucket: ${aws_s3_bucket.example.id}
      rule:
        object_ownership: ObjectWriter
```
