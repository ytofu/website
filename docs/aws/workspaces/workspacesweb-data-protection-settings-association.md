# Resource: aws_workspacesweb_data_protection_settings_association

ytofu resource for managing an AWS WorkSpaces Web Data Protection Settings Association.

## Basic Example

```yaml
resource:
  aws_workspacesweb_portal:
    example:
      display_name: example

resource:
  aws_workspacesweb_data_protection_settings:
    example:
      display_name: example

resource:
  aws_workspacesweb_data_protection_settings_association:
    example:
      data_protection_settings_arn: ${aws_workspacesweb_data_protection_settings.example.data_protection_settings_arn}
      portal_arn: ${aws_workspacesweb_portal.example.portal_arn}
```

## Argument Reference

The following arguments are required:

* `data_protection_settings_arn` - (Required) ARN of the data protection settings to associate with the portal. Forces replacement if changed.
* `portal_arn` - (Required) ARN of the portal to associate with the data protection settings. Forces replacement if changed.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports no additional attributes.
