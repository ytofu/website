# EC2 Transit Gateway Default Route Table Propagation

Manage EC2 Transit Gateway Default Route Table Propagation resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_transit_gateway_default_route_table_propagation:
    example:
      transit_gateway_id: ${aws_ec2_transit_gateway.example.id}
      transit_gateway_route_table_id: ${aws_ec2_transit_gateway_route_table.example.id}
```
