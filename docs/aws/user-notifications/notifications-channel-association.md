# Notifications Channel Association

Manage Notifications Channel Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_notifications_notification_configuration:
    example:
      name: example-notification-config
      description: Example notification configuration

resource:
  aws_notificationscontacts_email_contact:
    example:
      name: example-contact
      email_address: example@example.com

resource:
  aws_notifications_channel_association:
    example:
      arn: ${aws_notificationscontacts_email_contact.example.arn}
      notification_configuration_arn: ${aws_notifications_notification_configuration.example.arn}
```
