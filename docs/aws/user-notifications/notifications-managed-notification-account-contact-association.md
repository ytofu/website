# Resource: aws_notifications_managed_notification_account_contact_association

ytofu resource for managing an AWS User Notifications Managed Notification Account Contact Association. This resource associates an account contact with a managed notification configuration.

## Basic Example

```yaml
resource:
  aws_notifications_managed_notification_account_contact_association:
    example:
      contact_identifier: ACCOUNT_PRIMARY
      managed_notification_configuration_arn: "arn:aws:notifications::123456789012:managed-notification-configuration/category/AWS-Health/sub-category/Security"
```

## Argument Reference

The following arguments are required:

* `contact_identifier` - (Required) A unique value of an Account Contact Type to associate with the ManagedNotificationConfiguration. Valid values: `ACCOUNT_PRIMARY`, `ACCOUNT_ALTERNATE_BILLING`, `ACCOUNT_ALTERNATE_OPERATIONS`, `ACCOUNT_ALTERNATE_SECURITY`.
* `managed_notification_configuration_arn` - (Required) ARN of the managed notification configuration to associate the account contact with.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_notifications_managed_notification_account_contact_association.example arn:aws:notifications::123456789012:managed-notification-configuration/category/AWS-Health/sub-category/Security,ACCOUNT_PRIMARY
```
