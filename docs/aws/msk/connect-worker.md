# MSK Connect Worker Configuration

Create Kafka Connect worker configurations using ytofu YAML.

## Basic Worker Config

```yaml
resource:
  aws_mskconnect_worker_configuration:
    example:
      name: example
      properties_file_content: |
        key.converter=org.apache.kafka.connect.storage.StringConverter
        value.converter=org.apache.kafka.connect.storage.StringConverter
```
