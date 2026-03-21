# Default Route Table

Manage Default Route Table resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_default_route_table:
    example:
      default_route_table_id: ${aws_vpc.example.default_route_table_id}
      route:
        cidr_block: 10.0.1.0/24
        gateway_id: ${aws_internet_gateway.example.id}
      route:
        ipv6_cidr_block: "::/0"
        egress_only_gateway_id: ${aws_egress_only_internet_gateway.example.id}
      tags:
        Name: example
```
