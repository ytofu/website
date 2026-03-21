# Redshift Usage Limit

Manage Redshift Usage Limit resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_redshift_usage_limit:
    example:
      cluster_identifier: ${aws_redshift_cluster.example.id}
      feature_type: concurrency-scaling
      limit_type: time
      amount: 60
```
