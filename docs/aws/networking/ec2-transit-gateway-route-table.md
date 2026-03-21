# EC2 Transit Gateway Route Table

Manage EC2 Transit Gateway Route Table resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_transit_gateway_route_table:
    example:
      transit_gateway_id: ${aws_ec2_transit_gateway.example.id}
```
