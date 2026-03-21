# Resource: aws_notifications_managed_notification_additional_channel_association

ytofu resource for managing an AWS User Notifications Managed Notification Additional Channel Association. This resource associates a channel (such as an email contact, mobile device, or chat channel) with a managed notification.

## Basic Example

```yaml
resource:
  aws_notificationscontacts_email_contact:
    example:
      name: example-contact
      email_address: example@example.com

  aws_notifications_managed_notification_additional_channel_association:
    example:
      channel_arn: ${aws_notificationscontacts_email_contact.example.arn}
      managed_notification_arn: "arn:aws:notifications::123456789012:managed-notification-configuration/category/AWS-Health/sub-category/Security"```

## Argument Reference

The following arguments are required:

* `channel_arn` - (Required) ARN of the channel to associate with the managed notification.
* `managed_notification_arn` - (Required) ARN of the managed notification to associate the channel with.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_notifications_managed_notification_additional_channel_association.example arn:aws:notifications::123456789012:managed-notification-configuration/category/AWS-Health/sub-category/Security,arn:aws:notificationscontacts:us-west-2:123456789012:emailcontact:example-contact
```
