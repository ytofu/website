# EC2 Transit Gateway Multicast Group Member

Manage EC2 Transit Gateway Multicast Group Member resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_transit_gateway_multicast_group_member:
    example:
      group_ip_address: 224.0.0.1
      network_interface_id: ${aws_network_interface.example.id}
      transit_gateway_multicast_domain_id: ${aws_ec2_transit_gateway_multicast_domain.example.id}
```
