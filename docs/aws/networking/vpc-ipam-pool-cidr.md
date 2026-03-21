# VPC Ipam Pool CIDR

Manage VPC Ipam Pool CIDR resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_region:
    current:

resource:
  aws_vpc_ipam:
    example:
      operating_regions:
        region_name: ${data.aws_region.current.region}

resource:
  aws_vpc_ipam_pool:
    example:
      address_family: ipv4
      ipam_scope_id: ${aws_vpc_ipam.example.private_default_scope_id}
      locale: ${data.aws_region.current.region}

resource:
  aws_vpc_ipam_pool_cidr:
    example:
      ipam_pool_id: ${aws_vpc_ipam_pool.example.id}
      cidr: 172.20.0.0/16
```
