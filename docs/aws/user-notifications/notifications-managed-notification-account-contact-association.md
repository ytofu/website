# Notifications Managed Notification Account Contact Association

Manage Notifications Managed Notification Account Contact Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_notifications_managed_notification_account_contact_association:
    example:
      contact_identifier: ACCOUNT_PRIMARY
      managed_notification_configuration_arn: "arn:aws:notifications::123456789012:managed-notification-configuration/category/AWS-Health/sub-category/Security"
```
