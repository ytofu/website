# Docdb Global Cluster

Manage Docdb Global Cluster resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_docdb_global_cluster:
    example:
      global_cluster_identifier: global-test
      engine: docdb
      engine_version: 4.0.0

resource:
  aws_docdb_cluster:
    primary:
      engine: ${aws_docdb_global_cluster.example.engine}
      engine_version: ${aws_docdb_global_cluster.example.engine_version}
      cluster_identifier: test-primary-cluster
      master_username: username
      master_password: somepass123
      global_cluster_identifier: ${aws_docdb_global_cluster.example.id}
      db_subnet_group_name: default

resource:
  aws_docdb_cluster_instance:
    primary:
      engine: ${aws_docdb_global_cluster.example.engine}
      identifier: test-primary-cluster-instance
      cluster_identifier: ${aws_docdb_cluster.primary.id}
      instance_class: db.r5.large

resource:
  aws_docdb_cluster:
    secondary:
      engine: ${aws_docdb_global_cluster.example.engine}
      engine_version: ${aws_docdb_global_cluster.example.engine_version}
      cluster_identifier: test-secondary-cluster
      global_cluster_identifier: ${aws_docdb_global_cluster.example.id}
      db_subnet_group_name: default
      depends_on:
        - ${aws_docdb_cluster.primary}

resource:
  aws_docdb_cluster_instance:
    secondary:
      engine: ${aws_docdb_global_cluster.example.engine}
      identifier: test-secondary-cluster-instance
      cluster_identifier: ${aws_docdb_cluster.secondary.id}
      instance_class: db.r5.large
      depends_on:
        - ${aws_docdb_cluster_instance.primary}
```

## New Global Cluster From Existing DB Cluster

```yaml
resource:
  aws_docdb_cluster:
    example:
      lifecycle:
        ignore_changes: 
          - global_cluster_identifier

resource:
  aws_docdb_global_cluster:
    example:
      global_cluster_identifier: example
      source_db_cluster_identifier: ${aws_docdb_cluster.example.arn}
```
