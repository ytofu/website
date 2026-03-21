# Schemas Discoverer

Manage Schemas Discoverer resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudwatch_event_bus:
    messenger:
      name: chat-messages

resource:
  aws_schemas_discoverer:
    test:
      source_arn: ${aws_cloudwatch_event_bus.messenger.arn}
      description: Auto discover event schemas
```
