# Redshift Snapshot Copy

Manage Redshift Snapshot Copy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_redshift_snapshot_copy:
    example:
      cluster_identifier: ${aws_redshift_cluster.example.id}
      destination_region: us-east-1
```
