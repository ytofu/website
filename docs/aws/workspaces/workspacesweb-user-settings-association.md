# Resource: aws_workspacesweb_user_settings_association

ytofu resource for managing an AWS WorkSpaces Web User Settings Association.

## Basic Example

```yaml
resource:
  aws_workspacesweb_portal:
    example:
      display_name: example

  aws_workspacesweb_user_settings:
    example:
      copy_allowed: Enabled
      download_allowed: Enabled
      paste_allowed: Enabled
      print_allowed: Enabled
      upload_allowed: Enabled

  aws_workspacesweb_user_settings_association:
    example:
      user_settings_arn: ${aws_workspacesweb_user_settings.example.user_settings_arn}
      portal_arn: ${aws_workspacesweb_portal.example.portal_arn}```

## Argument Reference

The following arguments are required:

* `user_settings_arn` - (Required) ARN of the user settings to associate with the portal. Forces replacement if changed.
* `portal_arn` - (Required) ARN of the portal to associate with the user settings. Forces replacement if changed.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports no additional attributes.
