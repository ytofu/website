# Neptune Cluster Endpoint

Manage Neptune Cluster Endpoint resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_neptune_cluster_endpoint:
    example:
      cluster_identifier: ${aws_neptune_cluster.test.cluster_identifier}
      cluster_endpoint_identifier: example
      endpoint_type: READER
```
