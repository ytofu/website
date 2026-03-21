# MSK Topic

Manage MSK Topic resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_msk_topic:
    example:
      name: Example
      cluster_arn: ${aws_msk_cluster.example.arn}
      partition_count: 2
      replication_factor: 2
      configs: '{ "retention.ms" = "604800000" "retention.bytes" = "-1", "cleanup.policy" = "delete", "min.insync.replicas" = "2" }'
```
