# Quicksight Ingestion

Manage Quicksight Ingestion resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_quicksight_ingestion:
    example:
      data_set_id: ${aws_quicksight_data_set.example.data_set_id}
      ingestion_id: example-id
      ingestion_type: FULL_REFRESH
```
