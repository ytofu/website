# Datasync Location FSX Openzfs File System

Manage Datasync Location FSX Openzfs File System resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_datasync_location_fsx_openzfs_file_system:
    example:
      fsx_filesystem_arn: ${aws_fsx_openzfs_file_system.example.arn}
      security_group_arns: 
        - ${aws_security_group.example.arn}
      protocol:
        nfs:
          mount_options:
            version: AUTOMATIC
```
