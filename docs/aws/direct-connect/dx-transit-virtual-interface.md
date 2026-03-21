# DX Transit Virtual Interface

Manage DX Transit Virtual Interface resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_dx_gateway:
    example:
      name: tf-dxg-example
      amazon_side_asn: 64512

resource:
  aws_dx_transit_virtual_interface:
    example:
      connection_id: ${aws_dx_connection.example.id}
      dx_gateway_id: ${aws_dx_gateway.example.id}
      name: tf-transit-vif-example
      vlan: 4094
      address_family: ipv4
      bgp_asn: 65352
```
