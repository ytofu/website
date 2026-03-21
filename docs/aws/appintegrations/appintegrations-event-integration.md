# Appintegrations Event Integration

Manage Appintegrations Event Integration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appintegrations_event_integration:
    example:
      name: example-name
      description: Example Description
      eventbridge_bus: default
      event_filter:
        source: aws.partner/examplepartner.com
      tags: 
```
