# Resource: aws_notifications_channel_association

ytofu resource for managing an AWS User Notifications Channel Association. This resource associates a channel (such as an email contact) with a notification configuration.

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

## Argument Reference

The following arguments are required:

* `arn` - (Required) ARN of the channel to associate with the notification configuration. Must match pattern `^arn:aws:(chatbot|consoleapp|notifications-contacts):[a-zA-Z0-9-]*:[0-9]{12}:[a-zA-Z0-9-_.@]+/[a-zA-Z0-9/_.@:-]+$`.
* `notification_configuration_arn` - (Required) ARN of the notification configuration to associate the channel with.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_notifications_channel_association.example arn:aws:notifications:us-west-2:123456789012:configuration:example-notification-config,arn:aws:notificationscontacts:us-west-2:123456789012:emailcontact:example-contact
```
