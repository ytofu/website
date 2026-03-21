# Customer Gateway

Manage Customer Gateway resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_customer_gateway:
    main:
      bgp_asn: 65000
      ip_address: 172.83.124.10
      type: ipsec.1
      tags:
        Name: main-customer-gateway
```
