# EC2 Transit Gateway Prefix List Reference

Manage EC2 Transit Gateway Prefix List Reference resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_transit_gateway_prefix_list_reference:
    example:
      prefix_list_id: ${aws_ec2_managed_prefix_list.example.id}
      transit_gateway_attachment_id: ${aws_ec2_transit_gateway_vpc_attachment.example.id}
      transit_gateway_route_table_id: ${aws_ec2_transit_gateway.example.association_default_route_table_id}
```

## Blackhole Routing

```yaml
resource:
  aws_ec2_transit_gateway_prefix_list_reference:
    example:
      blackhole: true
      prefix_list_id: ${aws_ec2_managed_prefix_list.example.id}
      transit_gateway_route_table_id: ${aws_ec2_transit_gateway.example.association_default_route_table_id}
```
