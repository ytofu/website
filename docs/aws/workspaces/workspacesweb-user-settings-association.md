# Workspacesweb User Settings Association

Manage Workspacesweb User Settings Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_workspacesweb_portal:
    example:
      display_name: example

resource:
  aws_workspacesweb_user_settings:
    example:
      copy_allowed: Enabled
      download_allowed: Enabled
      paste_allowed: Enabled
      print_allowed: Enabled
      upload_allowed: Enabled

resource:
  aws_workspacesweb_user_settings_association:
    example:
      user_settings_arn: ${aws_workspacesweb_user_settings.example.user_settings_arn}
      portal_arn: ${aws_workspacesweb_portal.example.portal_arn}
```
