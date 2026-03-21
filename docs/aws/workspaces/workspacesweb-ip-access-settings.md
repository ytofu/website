# Workspacesweb IP Access Settings

Manage Workspacesweb IP Access Settings resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_workspacesweb_ip_access_settings:
    example:
      display_name: example
      ip_rule:
        ip_range: 10.0.0.0/16
```

## With Multiple IP Rules

```yaml
resource:
  aws_workspacesweb_ip_access_settings:
    example:
      display_name: example
      description: Example IP access settings
      ip_rule:
        ip_range: 10.0.0.0/16
        description: Main office
      ip_rule:
        ip_range: 192.168.0.0/24
        description: Branch office
```

## With All Arguments

```yaml
resource:
  aws_kms_key:
    example:
      description: KMS key for WorkSpaces Web IP Access Settings
      deletion_window_in_days: 7

resource:
  aws_workspacesweb_ip_access_settings:
    example:
      display_name: example
      description: Example IP access settings
      customer_managed_key: ${aws_kms_key.example.arn}
      additional_encryption_context:
        Environment: Production
      ip_rule:
        ip_range: 10.0.0.0/16
        description: Main office
      ip_rule:
        ip_range: 192.168.0.0/24
        description: Branch office
      tags:
        Name: example-ip-access-settings
```
