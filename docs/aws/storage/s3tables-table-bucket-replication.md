# S3tables Table Bucket Replication

Manage S3tables Table Bucket Replication resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3tables_table_bucket_replication:
    example:
      table_bucket_arn: ${aws_s3tables_table_bucket.source.arn}
      role: ${aws_iam_role.example.arn}
      rule:
        destination:
          destination_table_bucket_arn: ${aws_s3tables_table_bucket.target.arn}
```
