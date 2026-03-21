# Elasticache Parameter Group

Manage Elasticache Parameter Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_elasticache_parameter_group:
    default:
      name: cache-params
      family: redis2.8
      parameter:
        name: activerehashing
        value: yes
      parameter:
        name: min-slaves-to-write
        value: 2
```
