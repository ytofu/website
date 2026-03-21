# Docdbelastic Cluster

Manage Docdbelastic Cluster resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_docdbelastic_cluster:
    example:
      name: my-docdb-cluster
      admin_user_name: foo
      admin_user_password: mustbeeightchars
      auth_type: PLAIN_TEXT
      shard_capacity: 2
      shard_count: 1
```
