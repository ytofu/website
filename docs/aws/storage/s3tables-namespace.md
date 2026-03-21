# S3tables Namespace

Manage S3tables Namespace resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3tables_namespace:
    example:
      namespace: example_namespace
      table_bucket_arn: ${aws_s3tables_table_bucket.example.arn}

resource:
  aws_s3tables_table_bucket:
    example:
      name: example-bucket
```
