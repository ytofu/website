# EC2 Transit Gateway Peering Attachment

Manage EC2 Transit Gateway Peering Attachment resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_region:
    peer:

resource:
  aws_ec2_transit_gateway:
    local:
      tags:
        Name: Local TGW

resource:
  aws_ec2_transit_gateway:
    peer:
      tags:
        Name: Peer TGW

resource:
  aws_ec2_transit_gateway_peering_attachment:
    example:
      peer_account_id: ${aws_ec2_transit_gateway.peer.owner_id}
      peer_region: ${data.aws_region.peer.name}
      peer_transit_gateway_id: ${aws_ec2_transit_gateway.peer.id}
      transit_gateway_id: ${aws_ec2_transit_gateway.local.id}
      tags:
        Name: TGW Peering Requestor
```
