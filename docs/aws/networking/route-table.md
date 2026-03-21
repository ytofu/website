# Route Table

Manage Route Table resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_route_table:
    example:
      vpc_id: ${aws_vpc.example.id}
      route:
        cidr_block: 10.0.1.0/24
        gateway_id: ${aws_internet_gateway.example.id}
      route:
        ipv6_cidr_block: "::/0"
        egress_only_gateway_id: ${aws_egress_only_internet_gateway.example.id}
      tags:
        Name: example
```

## Adopting an existing local route

```yaml
resource:
  aws_vpc:
    test:
      cidr_block: 10.1.0.0/16

resource:
  aws_route_table:
    test:
      vpc_id: ${aws_vpc.test.id}
      route:
        cidr_block: 10.1.0.0/16
        gateway_id: local
```
