# RDS Cluster

Manage RDS Cluster resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_rds_cluster:
    default:
      cluster_identifier: aurora-cluster-demo
      engine: aurora-mysql
      engine_version: 5.7.mysql_aurora.2.03.2
      availability_zones: 
        - us-west-2a
        - us-west-2b
        - us-west-2c
      database_name: mydb
      master_username: foo
      master_password: must_be_eight_characters
      backup_retention_period: 5
      preferred_backup_window: "07:00-09:00"
```

## Aurora MySQL 1.x (MySQL 5.6)

```yaml
resource:
  aws_rds_cluster:
    default:
      cluster_identifier: aurora-cluster-demo
      availability_zones: 
        - us-west-2a
        - us-west-2b
        - us-west-2c
      database_name: mydb
      master_username: foo
      master_password: must_be_eight_characters
      backup_retention_period: 5
      preferred_backup_window: "07:00-09:00"
```

## Aurora with PostgreSQL engine

```yaml
resource:
  aws_rds_cluster:
    postgresql:
      cluster_identifier: aurora-cluster-demo
      engine: aurora-postgresql
      availability_zones: 
        - us-west-2a
        - us-west-2b
        - us-west-2c
      database_name: mydb
      master_username: foo
      master_password: must_be_eight_characters
      backup_retention_period: 5
      preferred_backup_window: "07:00-09:00"
```

## RDS Multi-AZ Cluster

```yaml
resource:
  aws_rds_cluster:
    example:
      cluster_identifier: example
      availability_zones: 
        - us-west-2a
        - us-west-2b
        - us-west-2c
      engine: mysql
      db_cluster_instance_class: db.r6gd.xlarge
      storage_type: io1
      allocated_storage: 100
      iops: 1000
      master_username: test
      master_password: mustbeeightcharaters
```

## RDS Serverless v2 Cluster

```yaml
resource:
  aws_rds_cluster:
    example:
      cluster_identifier: example
      engine: aurora-postgresql
      engine_mode: provisioned
      engine_version: 13.6
      database_name: test
      master_username: test
      master_password: must_be_eight_characters
      storage_encrypted: true
      serverlessv2_scaling_configuration:
        max_capacity: 1.0
        min_capacity: 0.0
        seconds_until_auto_pause: 3600

resource:
  aws_rds_cluster_instance:
    example:
      cluster_identifier: ${aws_rds_cluster.example.id}
      instance_class: db.serverless
      engine: ${aws_rds_cluster.example.engine}
      engine_version: ${aws_rds_cluster.example.engine_version}
```

## RDS/Aurora Managed Master Passwords via Secrets Manager, default KMS Key

```yaml
resource:
  aws_rds_cluster:
    test:
      cluster_identifier: example
      database_name: test
      manage_master_user_password: true
      master_username: test
```

## RDS/Aurora Managed Master Passwords via Secrets Manager, specific KMS Key

```yaml
resource:
  aws_kms_key:
    example:
      description: Example KMS Key

resource:
  aws_rds_cluster:
    test:
      cluster_identifier: example
      database_name: test
      manage_master_user_password: true
      master_username: test
      master_user_secret_kms_key_id: ${aws_kms_key.example.key_id}
```

## Global Cluster Restored From Snapshot

```yaml
data:
  aws_db_cluster_snapshot:
    example:
      db_cluster_identifier: example-original-cluster
      most_recent: true

resource:
  aws_rds_cluster:
    example:
      engine: aurora
      engine_version: 5.6.mysql_aurora.1.22.4
      cluster_identifier: example
      snapshot_identifier: ${data.aws_db_cluster_snapshot.example.id}
      lifecycle:
        ignore_changes: 
          - snapshot_identifier
          - global_cluster_identifier

resource:
  aws_rds_global_cluster:
    example:
      global_cluster_identifier: example
      source_db_cluster_identifier: ${aws_rds_cluster.example.arn}
      force_destroy: true
```
