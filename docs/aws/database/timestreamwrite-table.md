# Timestreamwrite Table

Manage Timestreamwrite Table resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_timestreamwrite_table:
    example:
      database_name: ${aws_timestreamwrite_database.example.database_name}
      table_name: example
```

## Full usage

```yaml
resource:
  aws_timestreamwrite_table:
    example:
      database_name: ${aws_timestreamwrite_database.example.database_name}
      table_name: example
      retention_properties:
        magnetic_store_retention_period_in_days: 30
        memory_store_retention_period_in_hours: 8
      tags:
        Name: example-timestream-table
```

## Customer-defined Partition Key

```yaml
resource:
  aws_timestreamwrite_table:
    example:
      database_name: ${aws_timestreamwrite_database.example.database_name}
      table_name: example
      schema:
        composite_partition_key:
          enforcement_in_record: REQUIRED
          name: attr1
          type: DIMENSION
```
