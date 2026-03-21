# VPN Gateway

Manage VPN Gateway resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpn_gateway:
    vpn_gw:
      vpc_id: ${aws_vpc.main.id}
      tags:
        Name: main
```
