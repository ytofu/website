# Elasticache Replication Group

Manage Elasticache Replication Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_elasticache_replication_group:
    example:
      automatic_failover_enabled: true
      preferred_cache_cluster_azs: 
        - us-west-2a
        - us-west-2b
      replication_group_id: tf-rep-group-1
      description: example description
      node_type: cache.m4.large
      num_cache_clusters: 2
      parameter_group_name: default.redis3.2
      port: 6379
```

## Redis OSS/Valkey Cluster Mode Enabled

```yaml
resource:
  aws_elasticache_replication_group:
    baz:
      replication_group_id: tf-redis-cluster
      description: example description
      node_type: cache.t2.small
      port: 6379
      parameter_group_name: default.redis3.2.cluster.on
      automatic_failover_enabled: true
      num_node_groups: 2
      replicas_per_node_group: 1
```

## Redis OSS/Valkey Cluster Mode Enabled with Node Group Configuration

```yaml
resource:
  aws_elasticache_replication_group:
    example:
      replication_group_id: tf-redis-cluster
      description: example description
      node_type: cache.t2.small
      port: 6379
      parameter_group_name: default.redis3.2.cluster.on
      automatic_failover_enabled: true
      num_node_groups: 2
      node_group_configuration:
        node_group_id: 0001
        primary_availability_zone: us-west-2a
        replica_availability_zones: 
          - us-west-2b
        replica_count: 1
        slots: 0-8191
      node_group_configuration:
        node_group_id: 0002
        primary_availability_zone: us-west-2b
        replica_availability_zones: 
          - us-west-2a
        replica_count: 1
        slots: 8192-16383
```

## Redis Log Delivery configuration

```yaml
resource:
  aws_elasticache_replication_group:
    test:
      replication_group_id: myreplicaciongroup
      description: test description
      node_type: cache.t3.small
      port: 6379
      apply_immediately: true
      auto_minor_version_upgrade: false
      maintenance_window: "tue:06:30-tue:07:30"
      snapshot_window: "01:00-02:00"
      log_delivery_configuration:
        destination: ${aws_cloudwatch_log_group.example.name}
        destination_type: cloudwatch-logs
        log_format: text
        log_type: slow-log
      log_delivery_configuration:
        destination: ${aws_kinesis_firehose_delivery_stream.example.name}
        destination_type: kinesis-firehose
        log_format: json
        log_type: engine-log
```

## Creating a secondary replication group for a global replication group

```yaml
resource:
  aws_elasticache_replication_group:
    secondary:
      replication_group_id: example-secondary
      description: secondary replication group
      global_replication_group_id: ${aws_elasticache_global_replication_group.example.global_replication_group_id}
      num_cache_clusters: 1

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
```

## Redis AUTH and In-Transit Encryption Enabled

```yaml
resource:
  aws_elasticache_replication_group:
    example:
      replication_group_id: example
      description: example with authentication
      node_type: cache.t2.micro
      num_cache_clusters: 1
      port: 6379
      subnet_group_name: ${aws_elasticache_subnet_group.example.name}
      security_group_ids: 
        - ${aws_security_group.example.id}
      parameter_group_name: default.redis5.0
      engine_version: 5.0.6
      transit_encryption_enabled: true
      auth_token: abcdefgh1234567890
      auth_token_update_strategy: ROTATE
```
