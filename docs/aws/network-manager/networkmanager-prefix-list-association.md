# Networkmanager Prefix List Association

Manage Networkmanager Prefix List Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_managed_prefix_list:
    prefix_list:
      name: example
      address_family: IPv4
      max_entries: 5
      entry:
        cidr: 10.0.0.0/8
        description: Example CIDR

resource:
  aws_networkmanager_prefix_list_association:
    pl_association:
      core_network_id: ${aws_networkmanager_core_network.core_network.id}
      prefix_list_arn: ${aws_ec2_managed_prefix_list.prefix_list.arn}
      prefix_list_alias: exampleprefixlist
```
