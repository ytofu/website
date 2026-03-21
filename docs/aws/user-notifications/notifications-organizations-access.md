# Resource: aws_notifications_organizations_access

ytofu resource for managing AWS User Notifications Organizations Access. This resource enables or disables organizations access for AWS User Notifications in AWS Organizations, allowing the service to access organization information.

## Basic Example

```yaml
resource:
  aws_notifications_organizations_access:
    example:
      enabled: true
```

## Argument Reference

The following arguments are required:

* `enabled` - (Required) Whether to enable organizations access for AWS User Notifications in AWS Organizations. When set to `true`, enables organizations access. When set to `false`, disables organizations access.

## Attribute Reference

This resource exports no additional attributes.

## Timeouts

Configuration options:

* `create` - (Default `10m`) How long to wait for the organizations access to be enabled or disabled during resource creation.
* `update` - (Default `10m`) How long to wait for the organizations access to be enabled or disabled during resource updates.
* `delete` - (Default `10m`) How long to wait for the organizations access to be disabled during resource deletion.

## Import

```bash
ytofu import aws_notifications_organizations_access.example 123456789012
```
