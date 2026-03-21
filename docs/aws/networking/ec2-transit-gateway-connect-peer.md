# EC2 Transit Gateway Connect Peer

Manage EC2 Transit Gateway Connect Peer resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_transit_gateway_connect:
    example:
      transport_attachment_id: ${aws_ec2_transit_gateway_vpc_attachment.example.id}
      transit_gateway_id: ${aws_ec2_transit_gateway.example.id}

resource:
  aws_ec2_transit_gateway_connect_peer:
    example:
      peer_address: 10.1.2.3
      inside_cidr_blocks: 
        - 169.254.100.0/29
      transit_gateway_attachment_id: ${aws_ec2_transit_gateway_connect.example.id}
```
