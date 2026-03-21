# DX Hosted Private Virtual Interface Accepter

Manage DX Hosted Private Virtual Interface Accepter resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    accepter:

resource:
  aws_dx_hosted_private_virtual_interface:
    creator:
      connection_id: dxcon-zzzzzzzz
      owner_account_id: ${data.aws_caller_identity.accepter.account_id}
      name: vif-foo
      vlan: 4094
      address_family: ipv4
      bgp_asn: 65352
      depends_on: 
        - ${aws_vpn_gateway.vpn_gw}

resource:
  aws_vpn_gateway:
    vpn_gw:

resource:
  aws_dx_hosted_private_virtual_interface_accepter:
    accepter:
      virtual_interface_id: ${aws_dx_hosted_private_virtual_interface.creator.id}
      vpn_gateway_id: ${aws_vpn_gateway.vpn_gw.id}
      tags:
        Side: Accepter
```
