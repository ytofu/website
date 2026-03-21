# Workspaces Workspace

Manage Workspaces Workspace resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_workspaces_bundle:
    value_windows_10:
      bundle_id: "wsb-bh8rsxt14" # Value with Windows 10 (English)

data:
  aws_kms_key:
    workspaces:
      key_id: alias/aws/workspaces

resource:
  aws_workspaces_workspace:
    example:
      directory_id: ${aws_workspaces_directory.example.id}
      bundle_id: ${data.aws_workspaces_bundle.value_windows_10.id}
      user_name: john.doe
      root_volume_encryption_enabled: true
      user_volume_encryption_enabled: true
      volume_encryption_key: ${data.aws_kms_key.workspaces.arn}
      workspace_properties:
        compute_type_name: VALUE
        user_volume_size_gib: 10
        root_volume_size_gib: 80
        running_mode: AUTO_STOP
        running_mode_auto_stop_timeout_in_minutes: 60
      tags:
        Department: IT
```
