# Notifications Notification Configuration

Manage Notifications Notification Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_notifications_notification_configuration:
    example:
      name: example
      description: Example notification configuration
      tags:
        Environment: production
        Project: example
```

## With Aggregation Duration

```yaml
resource:
  aws_notifications_notification_configuration:
    example:
      name: example-aggregation
      description: Example notification configuration with aggregation
      aggregation_duration: SHORT
      tags:
        Environment: production
        Project: example
```
