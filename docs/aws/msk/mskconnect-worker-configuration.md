# Mskconnect Worker Configuration

Manage Mskconnect Worker Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_mskconnect_worker_configuration:
    example:
      name: example
      properties_file_content: |
        key.converter=org.apache.kafka.connect.storage.StringConverter
        value.converter=org.apache.kafka.connect.storage.StringConverter
```
