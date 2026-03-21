# Workspacesweb Browser Settings

Manage Workspacesweb Browser Settings resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_workspacesweb_browser_settings:
    example:
      browser_policy: '{ "AdditionalSettings": { "DownloadsSettings": { "Behavior": "DISABLE" } } }'
```

## With All Arguments

```yaml
resource:
  aws_kms_key:
    example:
      description: KMS key for WorkSpaces Web Browser Settings
      deletion_window_in_days: 7

resource:
  aws_workspacesweb_browser_settings:
    example:
      browser_policy: '{ "chromePolicies": { "DefaultDownloadDirectory": { "value": "/home/as2-streaming-user/MyFiles/TemporaryFiles1" } } }'
      customer_managed_key: ${aws_kms_key.example.arn}
      additional_encryption_context:
        Environment: Production
      tags:
        Name: example-browser-settings
```
