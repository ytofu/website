# Notifications Event Rule

Manage Notifications Event Rule resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_notifications_notification_configuration:
    example:
      name: example
      description: example configuration

resource:
  aws_notifications_event_rule:
    example:
      event_pattern: '{ "detail": { "state": { "value": ["ALARM"] } } }'
      event_type: CloudWatch Alarm State Change
      notification_configuration_arn: ${aws_notifications_notification_configuration.example.arn}
      regions: 
        - us-east-1
        - us-west-2
      source: aws.cloudwatch
```
