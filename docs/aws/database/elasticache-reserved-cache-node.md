# Elasticache Reserved Cache Node

Manage Elasticache Reserved Cache Node resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_elasticache_reserved_cache_node_offering:
    example:
      cache_node_type: cache.t4g.small
      duration: P1Y
      offering_type: No Upfront
      product_description: redis

resource:
  aws_elasticache_reserved_cache_node:
    example:
      reserved_cache_nodes_offering_id: ${data.aws_elasticache_reserved_cache_node_offering.example.offering_id}
      id: optionalCustomReservationID
      cache_node_count: 3
```
