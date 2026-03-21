# EC2 Transit Gateway Policy Table Association

Manage EC2 Transit Gateway Policy Table Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_transit_gateway_policy_table_association:
    example:
      transit_gateway_attachment_id: ${aws_networkmanager_transit_gateway_peering.example.transit_gateway_peering_attachment_id}
      transit_gateway_policy_table_id: ${aws_ec2_transit_gateway_policy_table.example.id}
```
