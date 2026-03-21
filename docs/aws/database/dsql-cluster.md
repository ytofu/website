# Dsql Cluster

Manage Dsql Cluster resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_dsql_cluster:
    example:
      deletion_protection_enabled: true
      tags:
        Name: TestCluster
```
