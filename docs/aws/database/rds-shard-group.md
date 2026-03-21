# RDS Shard Group

Manage RDS Shard Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_rds_cluster:
    example:
      cluster_identifier: example-limitless-cluster
      engine: aurora-postgresql
      engine_version: 16.6-limitless
      engine_mode: 
      storage_type: aurora-iopt1
      cluster_scalability_type: limitless
      master_username: foo
      master_password: must_be_eight_characters
      performance_insights_enabled: true
      performance_insights_retention_period: 31
      enabled_cloudwatch_logs_exports: 
        - postgresql
      monitoring_interval: 5
      monitoring_role_arn: ${aws_iam_role.example.arn}

resource:
  aws_rds_shard_group:
    example:
      db_shard_group_identifier: example-shard-group
      db_cluster_identifier: ${aws_rds_cluster.example.id}
      max_acu: 1200
```
