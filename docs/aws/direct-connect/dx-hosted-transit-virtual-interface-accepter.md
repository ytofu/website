# DX Hosted Transit Virtual Interface Accepter

Manage DX Hosted Transit Virtual Interface Accepter resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    accepter:

resource:
  aws_dx_hosted_transit_virtual_interface:
    creator:
      connection_id: dxcon-zzzzzzzz
      owner_account_id: ${data.aws_caller_identity.accepter.account_id}
      name: tf-transit-vif-example
      vlan: 4094
      address_family: ipv4
      bgp_asn: 65352
      depends_on: 
        - ${aws_dx_gateway.example}

resource:
  aws_dx_gateway:
    example:
      name: tf-dxg-example
      amazon_side_asn: 64512

resource:
  aws_dx_hosted_transit_virtual_interface_accepter:
    accepter:
      virtual_interface_id: ${aws_dx_hosted_transit_virtual_interface.creator.id}
      dx_gateway_id: ${aws_dx_gateway.example.id}
      tags:
        Side: Accepter
```
