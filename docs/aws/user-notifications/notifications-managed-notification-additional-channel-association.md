# Notifications Managed Notification Additional Channel Association

Manage Notifications Managed Notification Additional Channel Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_notificationscontacts_email_contact:
    example:
      name: example-contact
      email_address: example@example.com

resource:
  aws_notifications_managed_notification_additional_channel_association:
    example:
      channel_arn: ${aws_notificationscontacts_email_contact.example.arn}
      managed_notification_arn: "arn:aws:notifications::123456789012:managed-notification-configuration/category/AWS-Health/sub-category/Security"
```
