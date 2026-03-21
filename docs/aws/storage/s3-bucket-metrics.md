# S3 Bucket Metrics

Configure request metrics for S3 buckets using ytofu YAML.

## Entire Bucket Metrics

```yaml
resource:
  aws_s3_bucket_metric:
    example:
      bucket: ${aws_s3_bucket.example.id}
      name: EntireBucket
```

## With Prefix Filter

```yaml
resource:
  aws_s3_bucket_metric:
    example:
      bucket: ${aws_s3_bucket.example.id}
      name: ImportantBlueDocuments
      filter:
        prefix: documents/
        tags:
          priority: high
          class: blue
```
