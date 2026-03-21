# Glue Crawler

Manage Glue Crawler resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_glue_crawler:
    example:
      database_name: ${aws_glue_catalog_database.example.name}
      name: example
      role: ${aws_iam_role.example.arn}
      dynamodb_target:
        path: table-name
```

## JDBC Target Example

```yaml
resource:
  aws_glue_crawler:
    example:
      database_name: ${aws_glue_catalog_database.example.name}
      name: example
      role: ${aws_iam_role.example.arn}
      jdbc_target:
        connection_name: ${aws_glue_connection.example.name}
        path: database-name/%
```

## S3 Target Example

```yaml
resource:
  aws_glue_crawler:
    example:
      database_name: ${aws_glue_catalog_database.example.name}
      name: example
      role: ${aws_iam_role.example.arn}
      s3_target:
        path: "s3://${aws_s3_bucket.example.bucket}"
```

## Catalog Target Example

```yaml
resource:
  aws_glue_crawler:
    example:
      database_name: ${aws_glue_catalog_database.example.name}
      name: example
      role: ${aws_iam_role.example.arn}
      catalog_target:
        database_name: ${aws_glue_catalog_database.example.name}
        tables: 
          - ${aws_glue_catalog_table.example.name}
      schema_change_policy:
        delete_behavior: LOG
      configuration: |
        {
        "Version":1.0,
        "Grouping": {
        "TableGroupingPolicy": "CombineCompatibleSchemas"
        }
        }
```

## MongoDB Target Example

```yaml
resource:
  aws_glue_crawler:
    example:
      database_name: ${aws_glue_catalog_database.example.name}
      name: example
      role: ${aws_iam_role.example.arn}
      mongodb_target:
        connection_name: ${aws_glue_connection.example.name}
        path: database-name/%
```

## Configuration Settings Example

```yaml
resource:
  aws_glue_crawler:
    events_crawler:
      database_name: ${aws_glue_catalog_database.glue_database.name}
      schedule: "cron(0 1 * * ? *)"
      name: "events_crawler_example-environment_name"
      role: ${aws_iam_role.glue_role.arn}
      tags: example-tags
      configuration: 'example-json-policy'
      s3_target:
        path: "s3://${aws_s3_bucket.data_lake_bucket.bucket}"
```
