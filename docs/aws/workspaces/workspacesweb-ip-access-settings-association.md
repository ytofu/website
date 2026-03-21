# Resource: aws_workspacesweb_ip_access_settings_association

ytofu resource for managing an AWS WorkSpaces Web IP Access Settings Association.

## Basic Example

```yaml
resource:
  aws_workspacesweb_portal:
    example:
      display_name: example

  aws_workspacesweb_ip_access_settings:
    example:
      display_name: example
      ip_rule:
        ip_range: 10.0.0.0/16

  aws_workspacesweb_ip_access_settings_association:
    example:
      ip_access_settings_arn: ${aws_workspacesweb_ip_access_settings.example.ip_access_settings_arn}
      portal_arn: ${aws_workspacesweb_portal.example.portal_arn}```

## Argument Reference

The following arguments are required:

* `ip_access_settings_arn` - (Required) ARN of the IP access settings to associate with the portal. Forces replacement if changed.
* `portal_arn` - (Required) ARN of the portal to associate with the IP access settings. Forces replacement if changed.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports no additional attributes.
