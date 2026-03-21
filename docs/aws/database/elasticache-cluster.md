# Elasticache Cluster

Manage Elasticache Cluster resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_elasticache_cluster:
    example:
      cluster_id: cluster-example
      engine: memcached
      node_type: cache.m4.large
      num_cache_nodes: 2
      parameter_group_name: default.memcached1.4
      port: 11211
```

## Redis Instance

```yaml
resource:
  aws_elasticache_cluster:
    example:
      cluster_id: cluster-example
      engine: redis
      node_type: cache.m4.large
      num_cache_nodes: 1
      parameter_group_name: default.redis3.2
      engine_version: 3.2.10
      port: 6379
```

## Redis Cluster Mode Disabled Read Replica Instance

```yaml
resource:
  aws_elasticache_cluster:
    replica:
      cluster_id: cluster-example
      replication_group_id: ${aws_elasticache_replication_group.example.id}
```

## Redis Log Delivery configuration

```yaml
resource:
  aws_elasticache_cluster:
    test:
      cluster_id: mycluster
      engine: redis
      node_type: cache.t3.micro
      num_cache_nodes: 1
      port: 6379
      apply_immediately: true
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

## Elasticache Cluster in Outpost

```yaml
data:
  aws_outposts_outposts:
    example:

data:
  aws_outposts_outpost:
    example:
      id: ${data.aws_outposts_outposts.example.ids[0]}

resource:
  aws_vpc:
    example:
      cidr_block: 10.0.0.0/16

resource:
  aws_subnet:
    example:
      vpc_id: ${aws_vpc.example.id}
      cidr_block: 10.0.1.0/24
      tags:
        Name: my-subnet

resource:
  aws_elasticache_subnet_group:
    example:
      name: my-cache-subnet
      subnet_ids: 
        - ${aws_subnet.example.id}

resource:
  aws_elasticache_cluster:
    example:
      cluster_id: cluster-example
      outpost_mode: single-outpost
      preferred_outpost_arn: ${data.aws_outposts_outpost.example.arn}
      engine: memcached
      node_type: cache.r5.large
      num_cache_nodes: 2
      parameter_group_name: default.memcached1.4
      port: 11211
      subnet_group_name: ${aws_elasticache_subnet_group.example.name}
```
