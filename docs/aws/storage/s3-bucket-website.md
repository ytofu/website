# S3 Bucket Website Configuration

Configure static website hosting on S3 buckets using ytofu YAML.

## Basic Website

```yaml
resource:
  aws_s3_bucket_website_configuration:
    example:
      bucket: ${aws_s3_bucket.example.id}
      index_document:
        suffix: index.html
      error_document:
        key: error.html
```

## With Routing Rules

```yaml
resource:
  aws_s3_bucket_website_configuration:
    example:
      bucket: ${aws_s3_bucket.example.id}
      index_document:
        suffix: index.html
      error_document:
        key: error.html
      routing_rule:
        - condition:
            key_prefix_equals: docs/
          redirect:
            replace_key_prefix_with: documents/
```

## Redirect All Requests

```yaml
resource:
  aws_s3_bucket_website_configuration:
    redirect:
      bucket: ${aws_s3_bucket.redirect.id}
      redirect_all_requests_to:
        host_name: example.com
        protocol: https
```
