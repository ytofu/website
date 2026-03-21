# DAX Parameter Group

Manage DAX Parameter Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_dax_parameter_group:
    example:
      name: example
      parameters:
        name: query-ttl-millis
        value: 100000
      parameters:
        name: record-ttl-millis
        value: 100000
```
