# S3tables Table Replication

Manage S3tables Table Replication resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3tables_table_replication:
    example:
      table_arn: ${aws_s3tables_table.example.arn}
      role: ${aws_iam_role.example.arn}
      rule:
        destination:
          destination_table_bucket_arn: ${aws_s3tables_table_bucket.target.arn}
```
