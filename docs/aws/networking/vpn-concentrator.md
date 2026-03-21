# VPN Concentrator

Manage VPN Concentrator resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_transit_gateway:
    example:
      description: example
      tags:
        Name: example

resource:
  aws_vpn_concentrator:
    example:
      type: ipsec.1
      transit_gateway_id: ${aws_ec2_transit_gateway.example.id}
      tags:
        Name: example
```
