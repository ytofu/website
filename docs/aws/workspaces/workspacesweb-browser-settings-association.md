# Workspacesweb Browser Settings Association

Manage Workspacesweb Browser Settings Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_workspacesweb_portal:
    example:
      display_name: example

resource:
  aws_workspacesweb_browser_settings:
    example:
      browser_policy: '{ "chromePolicies": { "DefaultDownloadDirectory": { "value": "/home/as2-streaming-user/MyFiles/TemporaryFiles1" } } }'

resource:
  aws_workspacesweb_browser_settings_association:
    example:
      browser_settings_arn: ${aws_workspacesweb_browser_settings.example.browser_settings_arn}
      portal_arn: ${aws_workspacesweb_portal.example.portal_arn}
```
