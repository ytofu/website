# Memorydb Snapshot

Manage Memorydb Snapshot resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_memorydb_snapshot:
    example:
      cluster_name: ${aws_memorydb_cluster.example.name}
      name: my-snapshot
```
