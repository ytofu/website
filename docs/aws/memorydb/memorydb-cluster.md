# Memorydb Cluster

Manage Memorydb Cluster resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_memorydb_cluster:
    example:
      acl_name: open-access
      name: my-cluster
      node_type: db.t4g.small
      engine: redis
      engine_version: 7.1
      num_shards: 2
      security_group_ids: 
        - ${aws_security_group.example.id}
      snapshot_retention_limit: 7
      subnet_group_name: ${aws_memorydb_subnet_group.example.id}
```
