# Resource: aws_networkmanager_prefix_list_association

Associates an EC2 managed prefix list with a Network Manager Cloud WAN core network. Once associated, the prefix list can be referenced in the core network policy document.

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

  aws_networkmanager_prefix_list_association:
    pl_association:
      core_network_id: ${aws_networkmanager_core_network.core_network.id}
      prefix_list_arn: ${aws_ec2_managed_prefix_list.prefix_list.arn}
      prefix_list_alias: exampleprefixlist```

## Argument Reference

The following arguments are required:

* `core_network_id` - (Required, Forces new resource) The ID of the core network to associate the prefix list with.
* `prefix_list_alias` - (Required, Forces new resource) An alias for the prefix list association. This alias can be used to reference the prefix list in the core network policy document. Must start with a letter, be less than 64 characters long, and may only include letters and numbers.
* `prefix_list_arn` - (Required, Forces new resource) The ARN of the EC2 managed prefix list to associate with the core network.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_networkmanager_prefix_list_association.example core-network-0fab1c1e1e1e1e1e1,arn:aws:ec2:us-west-2:123456789012:prefix-list/pl-0123456789abcdef0
```
