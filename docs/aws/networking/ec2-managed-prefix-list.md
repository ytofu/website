# EC2 Managed Prefix List

Manage EC2 Managed Prefix List resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_managed_prefix_list:
    example:
      name: All VPC CIDR-s
      address_family: IPv4
      max_entries: 5
      entry:
        cidr: ${aws_vpc.example.cidr_block}
        description: Primary
      entry:
        cidr: ${aws_vpc_ipv4_cidr_block_association.example.cidr_block}
        description: Secondary
      tags:
        Env: live
```
