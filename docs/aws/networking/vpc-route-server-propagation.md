# VPC Route Server Propagation

Manage VPC Route Server Propagation resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc_route_server_propagation:
    example:
      route_server_id: ${aws_vpc_route_server.example.route_server_id}
      route_table_id: ${aws_route_table.example.id}
```
