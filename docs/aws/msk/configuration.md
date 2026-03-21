# MSK Configuration

Create Kafka configurations using ytofu YAML.

## Basic Configuration

```yaml
resource:
  aws_msk_configuration:
    example:
      kafka_versions:
        - "3.5.1"
      name: example
      server_properties: |
        auto.create.topics.enable = true
        delete.topic.enable = true
        log.retention.hours = 168
```
