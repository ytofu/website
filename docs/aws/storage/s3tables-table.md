# S3tables Table

Manage S3tables Table resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3tables_table:
    example:
      name: example_table
      namespace: ${aws_s3tables_namespace.example.namespace}
      table_bucket_arn: ${aws_s3tables_namespace.example.table_bucket_arn}
      format: ICEBERG

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

## With Metadata Schema

```yaml
resource:
  aws_s3tables_table:
    example:
      name: example_table
      namespace: ${aws_s3tables_namespace.example.namespace}
      table_bucket_arn: ${aws_s3tables_namespace.example.table_bucket_arn}
      format: ICEBERG
      metadata:
        iceberg:
          schema:
            field:
              name: id
              type: long
              required: true
            field:
              name: name
              type: string
              required: true
            field:
              name: created_at
              type: timestamp
              required: false
            field:
              name: price
              type: decimal(10,2)
              required: false

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
