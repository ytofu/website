# Dataexchange Revision

Manage Dataexchange Revision resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_dataexchange_revision:
    example:
      data_set_id: ${aws_dataexchange_data_set.example.id}
```
