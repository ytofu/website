# Redshift Endpoint Access

Manage Redshift Endpoint Access resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_redshift_endpoint_access:
    example:
      endpoint_name: example
      subnet_group_name: ${aws_redshift_subnet_group.example.id}
      cluster_identifier: ${aws_redshift_cluster.example.cluster_identifier}
```
