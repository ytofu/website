# EC2 Transit Gateway Route

Manage EC2 Transit Gateway Route resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_transit_gateway_route:
    example:
      destination_cidr_block: 0.0.0.0/0
      transit_gateway_attachment_id: ${aws_ec2_transit_gateway_vpc_attachment.example.id}
      transit_gateway_route_table_id: ${aws_ec2_transit_gateway.example.association_default_route_table_id}
```

## Blackhole route

```yaml
resource:
  aws_ec2_transit_gateway_route:
    example:
      destination_cidr_block: 0.0.0.0/0
      blackhole: true
      transit_gateway_route_table_id: ${aws_ec2_transit_gateway.example.association_default_route_table_id}
```
