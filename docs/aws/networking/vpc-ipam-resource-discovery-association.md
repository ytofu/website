# VPC Ipam Resource Discovery Association

Manage VPC Ipam Resource Discovery Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc_ipam_resource_discovery_association:
    test:
      ipam_id: ${aws_vpc_ipam.test.id}
      ipam_resource_discovery_id: ${aws_vpc_ipam_resource_discovery.test.id}
      tags: 
```
