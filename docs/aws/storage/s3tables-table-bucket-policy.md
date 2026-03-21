# S3tables Table Bucket Policy

Manage S3tables Table Bucket Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3tables_table_bucket_policy:
    example:
      resource_policy: ${data.aws_iam_policy_document.example.json}
      table_bucket_arn: ${aws_s3tables_table_bucket.example.arn}

data:
  aws_iam_policy_document:
    example:
      statement:

resource:
  aws_s3tables_table_bucket:
    example:
      name: example-bucket
```
