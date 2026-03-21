# Route

Manage Route resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_route:
    r:
      route_table_id: ${aws_route_table.testing.id}
      destination_cidr_block: 10.0.1.0/22
      vpc_peering_connection_id: pcx-45ff3dc1
```
