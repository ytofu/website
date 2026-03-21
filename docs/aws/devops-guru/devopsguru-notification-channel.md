# Devopsguru Notification Channel

Manage Devopsguru Notification Channel resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_devopsguru_notification_channel:
    example:
      sns:
        topic_arn: ${aws_sns_topic.example.arn}
```

## Filters

```yaml
resource:
  aws_devopsguru_notification_channel:
    example:
      sns:
        topic_arn: ${aws_sns_topic.example.arn}
      filters:
        message_types: 
          - NEW_INSIGHT
        severities: 
          - HIGH
```
