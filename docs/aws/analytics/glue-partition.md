# Glue Partition

Manage Glue Partition resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_glue_partition:
    example:
      database_name: some-database
      table_name: some-table
      partition_values: 
        - some-value
```
