# Memorydb Multi Region Cluster

Manage Memorydb Multi Region Cluster resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_memorydb_multi_region_cluster:
    example:
      multi_region_cluster_name_suffix: example
      node_type: db.r7g.xlarge

resource:
  aws_memorydb_cluster:
    example:
      acl_name: ${aws_memorydb_acl.example.id}
      auto_minor_version_upgrade: false
      name: example
      node_type: db.t4g.small
      num_shards: 2
      security_group_ids: 
        - ${aws_security_group.example.id}
      snapshot_retention_limit: 7
      subnet_group_name: ${aws_memorydb_subnet_group.example.id}
      multi_region_cluster_name: ${aws_memorydb_multi_region_cluster.example.multi_region_cluster_name}
```
