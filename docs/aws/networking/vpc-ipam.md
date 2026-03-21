# VPC Ipam

Manage VPC Ipam resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_region:
    current:

resource:
  aws_vpc_ipam:
    main:
      description: My IPAM
      operating_regions:
        region_name: ${data.aws_region.current.region}
      tags:
        Test: Main
```
