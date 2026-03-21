# EC2 Transit Gateway Policy Table

Manage EC2 Transit Gateway Policy Table resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_transit_gateway_policy_table:
    example:
      transit_gateway_id: ${aws_ec2_transit_gateway.example.id}
      tags:
        Name: Example Policy Table
```
