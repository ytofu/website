# Quicksight User Custom Permission

Manage Quicksight User Custom Permission resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_quicksight_user_custom_permission:
    example:
      user_name: ${aws_quicksight_user.example.user_name}
      custom_permissions_name: ${aws_quicksight_custom_permissions.example.custom_permissions_name}
```
