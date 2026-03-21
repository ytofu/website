# Ssmincidents Replication Set

Manage Ssmincidents Replication Set resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ssmincidents_replication_set:
    replicationSetName:
      regions:
        name: us-west-2
      tags:
        exampleTag: exampleValue
```
