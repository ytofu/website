# Redshift Endpoint Authorization

Manage Redshift Endpoint Authorization resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_redshift_endpoint_authorization:
    example:
      account: 01234567910
      cluster_identifier: ${aws_redshift_cluster.example.cluster_identifier}
```
