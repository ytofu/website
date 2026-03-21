# Neptune Cluster Snapshot

Manage Neptune Cluster Snapshot resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_neptune_cluster_snapshot:
    example:
      db_cluster_identifier: ${aws_neptune_cluster.example.id}
      db_cluster_snapshot_identifier: resourcetestsnapshot1234
```
