# MSK Configuration

Manage MSK Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_msk_configuration:
    example:
      kafka_versions: 
        - 2.1.0
      name: example
      server_properties: |
        auto.create.topics.enable = true
        delete.topic.enable = true
```
