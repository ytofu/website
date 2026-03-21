# EBS Fast Snapshot Restore

Manage EBS Fast Snapshot Restore resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ebs_fast_snapshot_restore:
    example:
      availability_zone: us-west-2a
      snapshot_id: ${aws_ebs_snapshot.example.id}
```
