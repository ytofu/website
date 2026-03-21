# Neptune Parameter Group

Manage Neptune Parameter Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_neptune_parameter_group:
    example:
      family: neptune1
      name: example
      parameter:
        name: neptune_query_timeout
        value: 25
```
