# DX Hosted Transit Virtual Interface

Manage DX Hosted Transit Virtual Interface resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_dx_hosted_transit_virtual_interface:
    example:
      connection_id: ${aws_dx_connection.example.id}
      name: tf-transit-vif-example
      vlan: 4094
      address_family: ipv4
      bgp_asn: 65352
```
