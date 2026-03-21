# VPC Dhcp Options

Manage VPC Dhcp Options resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc_dhcp_options:
    dns_resolver:
      domain_name_servers: 
        - 8.8.8.8
        - 8.8.4.4
```
