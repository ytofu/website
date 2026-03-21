# RDS Cluster Snapshot Copy

Manage RDS Cluster Snapshot Copy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_rds_cluster:
    example:
      cluster_identifier: aurora-cluster-demo
      database_name: test
      engine: aurora-mysql
      master_username: tfacctest
      master_password: avoid-plaintext-passwords
      skip_final_snapshot: true

resource:
  aws_db_cluster_snapshot:
    example:
      db_cluster_identifier: ${aws_rds_cluster.example.cluster_identifier}
      db_cluster_snapshot_identifier: example

resource:
  aws_rds_cluster_snapshot_copy:
    example:
      source_db_cluster_snapshot_identifier: ${aws_db_cluster_snapshot.example.db_cluster_snapshot_arn}
      target_db_cluster_snapshot_identifier: example-copy
```
