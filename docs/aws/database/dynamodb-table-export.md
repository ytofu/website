# Dynamodb Table Export

Manage Dynamodb Table Export resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket_prefix: example
      force_destroy: true

resource:
  aws_dynamodb_table:
    example:
      name: example-table-1
      billing_mode: PAY_PER_REQUEST
      hash_key: user_id
      attribute:
        name: user_id
        type: S
      point_in_time_recovery:
        enabled: true

resource:
  aws_dynamodb_table_export:
    example:
      table_arn: ${aws_dynamodb_table.example.arn}
      s3_bucket: ${aws_s3_bucket.example.id}
```

## Example with export time

```yaml
resource:
  aws_dynamodb_table_export:
    example:
      export_time: "2023-04-02T11:30:13+01:00"
      s3_bucket: ${aws_s3_bucket.example.id}
      table_arn: ${aws_dynamodb_table.example.arn}
```

## Incremental export

```yaml
resource:
  aws_dynamodb_table_export:
    example:
      export_type: INCREMENTAL_EXPORT
      s3_bucket: ${aws_s3_bucket.example.id}
      table_arn: ${aws_dynamodb_table.example.arn}
      incremental_export_specification:
        export_from_time: "2025-02-09T12:00:00+01:00"
        export_to_time: "2025-02-09T13:00:00+01:00"
```
