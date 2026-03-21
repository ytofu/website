# Datasync Location EFS

Manage Datasync Location EFS resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_datasync_location_efs:
    example:
      efs_file_system_arn: ${aws_efs_mount_target.example.file_system_arn}
      ec2_config:
        security_group_arns: 
          - ${aws_security_group.example.arn}
        subnet_arn: ${aws_subnet.example.arn}
```
