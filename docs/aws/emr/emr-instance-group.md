# EMR Instance Group

Manage EMR Instance Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_emr_instance_group:
    task:
      cluster_id: ${aws_emr_cluster.tf-test-cluster.id}
      instance_count: 1
      instance_type: m5.xlarge
      name: my little instance group
```
