# Redshift Partner

Manage Redshift Partner resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_redshift_partner:
    example:
      cluster_identifier: ${aws_redshift_cluster.example.id}
      account_id: 01234567910
      database_name: ${aws_redshift_cluster.example.database_name}
      partner_name: example
```
