# Resource: aws_ec2_managed_prefix_list_entry

Use the `aws_prefix_list_entry` resource to manage a managed prefix list entry.

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `cidr` - (Required) CIDR block of this entry.
* `description` - (Optional) Description of this entry. Please note that due to API limitations, updating only the description of an entry will require recreating the entry.
* `prefix_list_id` - (Required) The ID of the prefix list.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - ID of the managed prefix list entry.

## Import

```bash
ytofu import aws_ec2_managed_prefix_list_entry.default pl-0570a1d2d725c16be,10.0.3.0/24
```
