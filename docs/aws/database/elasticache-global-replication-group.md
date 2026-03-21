# Elasticache Global Replication Group

Manage Elasticache Global Replication Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_elasticache_global_replication_group:
    example:
      global_replication_group_id_suffix: example
      primary_replication_group_id: ${aws_elasticache_replication_group.primary.id}

resource:
  aws_elasticache_replication_group:
    primary:
      replication_group_id: example-primary
      description: primary replication group
      engine: redis
      engine_version: 5.0.6
      node_type: cache.m5.large
      num_cache_clusters: 1

resource:
  aws_elasticache_replication_group:
    secondary:
      replication_group_id: example-secondary
      description: secondary replication group
      global_replication_group_id: ${aws_elasticache_global_replication_group.example.global_replication_group_id}
      num_cache_clusters: 1
```

## Managing Redis OOS/Valkey Engine Versions

```yaml
resource:
  aws_elasticache_global_replication_group:
    example:
      global_replication_group_id_suffix: example
      primary_replication_group_id: ${aws_elasticache_replication_group.primary.id}
      engine_version: 6.2

resource:
  aws_elasticache_replication_group:
    primary:
      replication_group_id: example-primary
      description: primary replication group
      engine: redis
      engine_version: 6.0
      node_type: cache.m5.large
      num_cache_clusters: 1

resource:
  aws_elasticache_replication_group:
    secondary:
      replication_group_id: example-secondary
      description: secondary replication group
      global_replication_group_id: ${aws_elasticache_global_replication_group.example.global_replication_group_id}
      num_cache_clusters: 1
```
