# Resource: aws_workspacesweb_browser_settings_association

ytofu resource for managing an AWS WorkSpaces Web Browser Settings Association.

## Basic Example

```yaml
resource:
  aws_workspacesweb_portal:
    example:
      display_name: example

  aws_workspacesweb_browser_settings:
    example:
      browser_policy: '{ "chromePolicies": { "DefaultDownloadDirectory": { "value": "/home/as2-streaming-user/MyFiles/TemporaryFiles1" } } }'

  aws_workspacesweb_browser_settings_association:
    example:
      browser_settings_arn: ${aws_workspacesweb_browser_settings.example.browser_settings_arn}
      portal_arn: ${aws_workspacesweb_portal.example.portal_arn}```

## Argument Reference

The following arguments are required:

* `browser_settings_arn` - (Required) ARN of the browser settings to associate with the portal. Forces replacement if changed.
* `portal_arn` - (Required) ARN of the portal to associate with the browser settings. Forces replacement if changed.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_workspacesweb_browser_settings_association.example arn:aws:workspaces-web:us-west-2:123456789012:browserSettings/browser_settings-id-12345678,arn:aws:workspaces-web:us-west-2:123456789012:portal/portal-id-12345678
```
