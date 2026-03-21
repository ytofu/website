# RDS Global Cluster

Manage RDS Global Cluster resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_rds_global_cluster:
    example:
      global_cluster_identifier: global-test
      engine: aurora
      engine_version: 5.6.mysql_aurora.1.22.2
      database_name: example_db

resource:
  aws_rds_cluster:
    primary:
      engine: ${aws_rds_global_cluster.example.engine}
      engine_version: ${aws_rds_global_cluster.example.engine_version}
      cluster_identifier: test-primary-cluster
      master_username: username
      master_password: somepass123
      database_name: example_db
      global_cluster_identifier: ${aws_rds_global_cluster.example.id}
      db_subnet_group_name: default

resource:
  aws_rds_cluster_instance:
    primary:
      engine: ${aws_rds_global_cluster.example.engine}
      engine_version: ${aws_rds_global_cluster.example.engine_version}
      identifier: test-primary-cluster-instance
      cluster_identifier: ${aws_rds_cluster.primary.id}
      instance_class: db.r4.large
      db_subnet_group_name: default

resource:
  aws_rds_cluster:
    secondary:
      engine: ${aws_rds_global_cluster.example.engine}
      engine_version: ${aws_rds_global_cluster.example.engine_version}
      cluster_identifier: test-secondary-cluster
      global_cluster_identifier: ${aws_rds_global_cluster.example.id}
      db_subnet_group_name: default
      lifecycle:
        ignore_changes:
          - replication_source_identifier
      depends_on:
        - ${aws_rds_cluster_instance.primary}

resource:
  aws_rds_cluster_instance:
    secondary:
      engine: ${aws_rds_global_cluster.example.engine}
      engine_version: ${aws_rds_global_cluster.example.engine_version}
      identifier: test-secondary-cluster-instance
      cluster_identifier: ${aws_rds_cluster.secondary.id}
      instance_class: db.r4.large
      db_subnet_group_name: default
```

## New PostgreSQL Global Cluster

```yaml
resource:
  aws_rds_global_cluster:
    example:
      global_cluster_identifier: global-test
      engine: aurora-postgresql
      engine_version: 11.9
      database_name: example_db

resource:
  aws_rds_cluster:
    primary:
      engine: ${aws_rds_global_cluster.example.engine}
      engine_version: ${aws_rds_global_cluster.example.engine_version}
      cluster_identifier: test-primary-cluster
      master_username: username
      master_password: somepass123
      database_name: example_db
      global_cluster_identifier: ${aws_rds_global_cluster.example.id}
      db_subnet_group_name: default

resource:
  aws_rds_cluster_instance:
    primary:
      engine: ${aws_rds_global_cluster.example.engine}
      engine_version: ${aws_rds_global_cluster.example.engine_version}
      identifier: test-primary-cluster-instance
      cluster_identifier: ${aws_rds_cluster.primary.id}
      instance_class: db.r4.large
      db_subnet_group_name: default

resource:
  aws_rds_cluster:
    secondary:
      engine: ${aws_rds_global_cluster.example.engine}
      engine_version: ${aws_rds_global_cluster.example.engine_version}
      cluster_identifier: test-secondary-cluster
      global_cluster_identifier: ${aws_rds_global_cluster.example.id}
      skip_final_snapshot: true
      db_subnet_group_name: default
      lifecycle:
        ignore_changes:
          - replication_source_identifier
      depends_on:
        - ${aws_rds_cluster_instance.primary}

resource:
  aws_rds_cluster_instance:
    secondary:
      engine: ${aws_rds_global_cluster.example.engine}
      engine_version: ${aws_rds_global_cluster.example.engine_version}
      identifier: test-secondary-cluster-instance
      cluster_identifier: ${aws_rds_cluster.secondary.id}
      instance_class: db.r4.large
      db_subnet_group_name: default
```

## New Global Cluster From Existing DB Cluster

```yaml
resource:
  aws_rds_cluster:
    example:
      lifecycle:
        ignore_changes: 
          - global_cluster_identifier

resource:
  aws_rds_global_cluster:
    example:
      force_destroy: true
      global_cluster_identifier: example
      source_db_cluster_identifier: ${aws_rds_cluster.example.arn}
```

## Upgrading Engine Versions

```yaml
resource:
  aws_rds_global_cluster:
    example:
      global_cluster_identifier: kyivkharkiv
      engine: aurora-mysql
      engine_version: 5.7.mysql_aurora.2.07.5

resource:
  aws_rds_cluster:
    primary:
      allow_major_version_upgrade: true
      apply_immediately: true
      cluster_identifier: odessadnipro
      database_name: totoro
      engine: ${aws_rds_global_cluster.example.engine}
      engine_version: ${aws_rds_global_cluster.example.engine_version}
      global_cluster_identifier: ${aws_rds_global_cluster.example.id}
      master_password: satsukimae
      master_username: maesatsuki
      skip_final_snapshot: true
      lifecycle:
        ignore_changes: 
          - engine_version

resource:
  aws_rds_cluster_instance:
    primary:
      apply_immediately: true
      cluster_identifier: ${aws_rds_cluster.primary.id}
      engine: ${aws_rds_cluster.primary.engine}
      engine_version: ${aws_rds_cluster.primary.engine_version}
      identifier: donetsklviv
      instance_class: db.r4.large
```
