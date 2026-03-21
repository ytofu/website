# DB Cluster Snapshot

Manage DB Cluster Snapshot resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_db_cluster_snapshot:
    example:
      db_cluster_identifier: ${aws_rds_cluster.example.id}
      db_cluster_snapshot_identifier: resourcetestsnapshot1234
```
