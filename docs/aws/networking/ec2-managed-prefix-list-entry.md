# EC2 Managed Prefix List Entry

Manage EC2 Managed Prefix List Entry resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_managed_prefix_list:
    example:
      name: All VPC CIDR-s
      address_family: IPv4
      max_entries: 5
      tags:
        Env: live

resource:
  aws_ec2_managed_prefix_list_entry:
    entry_1:
      cidr: ${aws_vpc.example.cidr_block}
      description: Primary
      prefix_list_id: ${aws_ec2_managed_prefix_list.example.id}
```
