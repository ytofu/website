# Datasync Location FSX Windows File System

Manage Datasync Location FSX Windows File System resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_datasync_location_fsx_windows_file_system:
    example:
      fsx_filesystem_arn: ${aws_fsx_windows_file_system.example.arn}
      user: SomeUser
      password: SuperSecretPassw0rd
      security_group_arns: 
        - ${aws_security_group.example.arn}
```
