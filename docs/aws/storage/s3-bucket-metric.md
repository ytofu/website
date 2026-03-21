# S3 Bucket Metric

Manage S3 Bucket Metric resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: example

resource:
  aws_s3_bucket_metric:
    example-entire-bucket:
      bucket: ${aws_s3_bucket.example.id}
      name: EntireBucket
```

## Add metrics configuration with S3 object filter

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: example

resource:
  aws_s3_bucket_metric:
    example-filtered:
      bucket: ${aws_s3_bucket.example.id}
      name: ImportantBlueDocuments
      filter:
        prefix: documents/
        tags:
          priority: high
          class: blue
```

## Add metrics configuration with S3 object filter for S3 Access Point

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: example

resource:
  aws_s3_access_point:
    example-access-point:
      bucket: ${aws_s3_bucket.example.id}
      name: example-access-point

resource:
  aws_s3_bucket_metric:
    example-filtered:
      bucket: ${aws_s3_bucket.example.id}
      name: ImportantBlueDocuments
      filter:
        access_point: ${aws_s3_access_point.example-access-point.arn}
        tags:
          priority: high
          class: blue
```
