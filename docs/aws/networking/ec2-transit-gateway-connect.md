# EC2 Transit Gateway Connect

Manage EC2 Transit Gateway Connect resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_transit_gateway_vpc_attachment:
    example:
      subnet_ids: 
        - ${aws_subnet.example.id}
      transit_gateway_id: ${aws_ec2_transit_gateway.example.id}
      vpc_id: ${aws_vpc.example.id}

resource:
  aws_ec2_transit_gateway_connect:
    attachment:
      transport_attachment_id: ${aws_ec2_transit_gateway_vpc_attachment.example.id}
      transit_gateway_id: ${aws_ec2_transit_gateway.example.id}
```
