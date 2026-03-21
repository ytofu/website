# Docdb Cluster Parameter Group

Manage Docdb Cluster Parameter Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_docdb_cluster_parameter_group:
    example:
      family: docdb3.6
      name: example
      description: docdb cluster parameter group
      parameter:
        name: tls
        value: enabled
```
