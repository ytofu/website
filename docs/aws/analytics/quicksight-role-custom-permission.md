# Quicksight Role Custom Permission

Manage Quicksight Role Custom Permission resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_quicksight_role_custom_permission:
    example:
      role: READER
      custom_permissions_name: ${aws_quicksight_custom_permissions.example.custom_permissions_name}
```
