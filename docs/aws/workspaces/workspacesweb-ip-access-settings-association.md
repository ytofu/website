# Workspacesweb IP Access Settings Association

Manage Workspacesweb IP Access Settings Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_workspacesweb_portal:
    example:
      display_name: example

resource:
  aws_workspacesweb_ip_access_settings:
    example:
      display_name: example
      ip_rule:
        ip_range: 10.0.0.0/16

resource:
  aws_workspacesweb_ip_access_settings_association:
    example:
      ip_access_settings_arn: ${aws_workspacesweb_ip_access_settings.example.ip_access_settings_arn}
      portal_arn: ${aws_workspacesweb_portal.example.portal_arn}
```
