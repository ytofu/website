# EFS Access Point

Manage EFS Access Point resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_efs_access_point:
    test:
      file_system_id: ${aws_efs_file_system.foo.id}
```
