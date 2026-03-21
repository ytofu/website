# NAT Gateway EIP Association

Manage NAT Gateway EIP Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_nat_gateway_eip_association:
    example:
      allocation_id: ${aws_eip.example.id}
      nat_gateway_id: ${aws_nat_gateway.example.id}
```
