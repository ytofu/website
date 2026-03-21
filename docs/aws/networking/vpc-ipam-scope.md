# VPC Ipam Scope

Manage VPC Ipam Scope resources using ytofu YAML.

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
  aws_vpc_ipam_scope:
    example:
      ipam_id: ${aws_vpc_ipam.example.id}
      description: Another Scope
```
