# VPC Endpoint Route Table Association

Manage VPC Endpoint Route Table Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc_endpoint_route_table_association:
    example:
      route_table_id: ${aws_route_table.example.id}
      vpc_endpoint_id: ${aws_vpc_endpoint.example.id}
```
