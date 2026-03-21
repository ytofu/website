# EFS Replication Configuration

Manage EFS Replication Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_efs_file_system:
    example:

resource:
  aws_efs_replication_configuration:
    example:
      source_file_system_id: ${aws_efs_file_system.example.id}
      destination:
        region: us-west-2
```
