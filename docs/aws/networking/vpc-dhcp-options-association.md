# VPC Dhcp Options Association

Manage VPC Dhcp Options Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc_dhcp_options_association:
    dns_resolver:
      vpc_id: ${aws_vpc.foo.id}
      dhcp_options_id: ${aws_vpc_dhcp_options.foo.id}
```
