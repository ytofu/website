# Workspacesweb Data Protection Settings Association

Manage Workspacesweb Data Protection Settings Association resources using ytofu YAML.

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
