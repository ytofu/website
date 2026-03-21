# Resource: aws_notifications_notification_hub

ytofu resource for managing an AWS User Notifications Notification Hub.

## Basic Example

```yaml
resource:
  aws_notifications_notification_hub:
    example:
      notification_hub_region: us-west-2
```

## Argument Reference

The following arguments are required:

* `notification_hub_region` - Notification Hub region.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_notifications_notification_hub.example us-west-2
```
