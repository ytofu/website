# Networkmanager Transit Gateway Route Table Attachment

Manage Networkmanager Transit Gateway Route Table Attachment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_networkmanager_transit_gateway_route_table_attachment:
    example:
      peering_id: ${aws_networkmanager_transit_gateway_peering.example.id}
      transit_gateway_route_table_arn: ${aws_ec2_transit_gateway_route_table.example.arn}
```
