# Neptune Cluster Parameter Group

Manage Neptune Cluster Parameter Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_neptune_cluster_parameter_group:
    example:
      family: neptune1
      name: example
      description: neptune cluster parameter group
      parameter:
        name: neptune_enable_audit_log
        value: 1
```
