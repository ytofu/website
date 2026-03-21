# Neptune Global Cluster

Manage Neptune Global Cluster resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_neptune_global_cluster:
    example:
      global_cluster_identifier: global-test
      engine: neptune
      engine_version: 1.2.0.0

resource:
  aws_neptune_cluster:
    primary:
      engine: ${aws_neptune_global_cluster.example.engine}
      engine_version: ${aws_neptune_global_cluster.example.engine_version}
      cluster_identifier: test-primary-cluster
      global_cluster_identifier: ${aws_neptune_global_cluster.example.id}
      neptune_subnet_group_name: default

resource:
  aws_neptune_cluster_instance:
    primary:
      engine: ${aws_neptune_global_cluster.example.engine}
      engine_version: ${aws_neptune_global_cluster.example.engine_version}
      identifier: test-primary-cluster-instance
      cluster_identifier: ${aws_neptune_cluster.primary.id}
      instance_class: db.r5.large
      neptune_subnet_group_name: default

resource:
  aws_neptune_cluster:
    secondary:
      engine: ${aws_neptune_global_cluster.example.engine}
      engine_version: ${aws_neptune_global_cluster.example.engine_version}
      cluster_identifier: test-secondary-cluster
      global_cluster_identifier: ${aws_neptune_global_cluster.example.id}
      neptune_subnet_group_name: default

resource:
  aws_neptune_cluster_instance:
    secondary:
      engine: ${aws_neptune_global_cluster.example.engine}
      engine_version: ${aws_neptune_global_cluster.example.engine_version}
      identifier: test-secondary-cluster-instance
      cluster_identifier: ${aws_neptune_cluster.secondary.id}
      instance_class: db.r5.large
      neptune_subnet_group_name: default
      depends_on:
        - ${aws_neptune_cluster_instance.primary}
```

## New Global Cluster From Existing DB Cluster

```yaml
resource:
  aws_neptune_cluster:
    example:
      lifecycle:
        ignore_changes: 
          - global_cluster_identifier

resource:
  aws_neptune_global_cluster:
    example:
      global_cluster_identifier: example
      source_db_cluster_identifier: ${aws_neptune_cluster.example.arn}
```
