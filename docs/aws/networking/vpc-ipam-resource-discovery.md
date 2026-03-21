# VPC Ipam Resource Discovery

Manage VPC Ipam Resource Discovery resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_region:
    current:

resource:
  aws_vpc_ipam_resource_discovery:
    main:
      description: My IPAM Resource Discovery
      operating_regions:
        region_name: ${data.aws_region.current.region}
      tags:
        Test: Main
```
