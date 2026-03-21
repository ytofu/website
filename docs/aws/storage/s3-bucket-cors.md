# S3 Bucket CORS Configuration

Configure cross-origin resource sharing for S3 buckets using ytofu YAML.

## Basic CORS

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: mybucket

  aws_s3_bucket_cors_configuration:
    example:
      bucket: ${aws_s3_bucket.example.id}
      cors_rule:
        - allowed_headers:
            - "*"
          allowed_methods:
            - PUT
            - POST
          allowed_origins:
            - https://s3-website-test.example.com
          expose_headers:
            - ETag
          max_age_seconds: 3000
        - allowed_methods:
            - GET
          allowed_origins:
            - "*"
```
