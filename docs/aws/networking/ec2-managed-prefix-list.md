# Resource: aws_ec2_managed_prefix_list

Provides a managed prefix list resource.

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `address_family` - (Required, Forces new resource) Address family (`IPv4` or `IPv6`) of this prefix list.
* `entry` - (Optional) Configuration block for prefix list entry. Detailed below. Different entries may have overlapping CIDR blocks, but a particular CIDR should not be duplicated.
* `max_entries` - (Required) Maximum number of entries that this prefix list can contain.
* `name` - (Required) Name of this resource. The name must not start with `com.amazonaws`.
* `tags` - (Optional) Map of tags to assign to this resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### `entry`

* `cidr` - (Required) CIDR block of this entry.
* `description` - (Optional) Description of this entry. Due to API limitations, updating only the description of an existing entry requires temporarily removing and re-adding the entry.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the prefix list.
* `id` - ID of the prefix list.
* `owner_id` - ID of the AWS account that owns this prefix list.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
* `version` - Latest version of this prefix list.

## Import

```bash
ytofu import aws_ec2_managed_prefix_list.default pl-0570a1d2d725c16be
```
