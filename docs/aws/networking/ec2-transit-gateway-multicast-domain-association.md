# EC2 Transit Gateway Multicast Domain Association

Manage EC2 Transit Gateway Multicast Domain Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_transit_gateway:
    example:
      multicast_support: enable

resource:
  aws_ec2_transit_gateway_vpc_attachment:
    example:
      subnet_ids: 
        - ${aws_subnet.example.id}
      transit_gateway_id: ${aws_ec2_transit_gateway.example.id}
      vpc_id: ${aws_vpc.example.id}

resource:
  aws_ec2_transit_gateway_multicast_domain:
    example:
      transit_gateway_id: ${aws_ec2_transit_gateway.example.id}

resource:
  aws_ec2_transit_gateway_multicast_domain_association:
    example:
      subnet_id: ${aws_subnet.example.id}
      transit_gateway_attachment_id: ${aws_ec2_transit_gateway_vpc_attachment.example.id}
      transit_gateway_multicast_domain_id: ${aws_ec2_transit_gateway_multicast_domain.example.id}
```
