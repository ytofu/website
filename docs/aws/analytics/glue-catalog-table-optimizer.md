# Glue Catalog Table Optimizer

Manage Glue Catalog Table Optimizer resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_glue_catalog_table_optimizer:
    example:
      catalog_id: 123456789012
      database_name: example_database
      table_name: example_table
      configuration:
        role_arn: "arn:aws:iam::123456789012:role/example-role"
        enabled: true
      type: compaction
```

## Snapshot Retention Optimizer

```yaml
resource:
  aws_glue_catalog_table_optimizer:
    example:
      catalog_id: 123456789012
      database_name: example_database
      table_name: example_table
      configuration:
        role_arn: "arn:aws:iam::123456789012:role/example-role"
        enabled: true
        retention_configuration:
          iceberg_configuration:
            snapshot_retention_period_in_days: 7
            number_of_snapshots_to_retain: 3
            clean_expired_files: true
      type: retention
```

## Orphan File Deletion Optimizer

```yaml
resource:
  aws_glue_catalog_table_optimizer:
    example:
      catalog_id: 123456789012
      database_name: example_database
      table_name: example_table
      configuration:
        role_arn: "arn:aws:iam::123456789012:role/example-role"
        enabled: true
        orphan_file_deletion_configuration:
          iceberg_configuration:
            orphan_file_retention_period_in_days: 7
            location: "s3://example-bucket/example_table/"
      type: orphan_file_deletion
```
