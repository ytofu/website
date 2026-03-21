# DX Hosted Public Virtual Interface Accepter

Manage DX Hosted Public Virtual Interface Accepter resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    accepter:

resource:
  aws_dx_hosted_public_virtual_interface:
    creator:
      connection_id: dxcon-zzzzzzzz
      owner_account_id: ${data.aws_caller_identity.accepter.account_id}
      name: vif-foo
      vlan: 4094
      address_family: ipv4
      bgp_asn: 65352
      customer_address: 175.45.176.1/30
      amazon_address: 175.45.176.2/30
      route_filter_prefixes:
        - 210.52.109.0/24
        - 175.45.176.0/22

resource:
  aws_dx_hosted_public_virtual_interface_accepter:
    accepter:
      virtual_interface_id: ${aws_dx_hosted_public_virtual_interface.creator.id}
      tags:
        Side: Accepter
```
