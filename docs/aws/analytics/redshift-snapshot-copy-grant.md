# Redshift Snapshot Copy Grant

Manage Redshift Snapshot Copy Grant resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_redshift_snapshot_copy_grant:
    test:
      snapshot_copy_grant_name: my-grant

resource:
  aws_redshift_cluster:
    test:
      snapshot_copy:
        destination_region: us-east-2
        grant_name: ${aws_redshift_snapshot_copy_grant.test.snapshot_copy_grant_name}
```
