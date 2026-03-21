# Memorydb Parameter Group

Manage Memorydb Parameter Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_memorydb_parameter_group:
    example:
      name: my-parameter-group
      family: memorydb_redis6
      parameter:
        name: activedefrag
        value: yes
```
