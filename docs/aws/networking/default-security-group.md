# Resource: aws_default_security_group

Provides a resource to manage a default security group. This resource can manage the default security group of the default or a non-default VPC.

## Basic Example

```yaml
resource:
  aws_vpc:
    mainvpc:
      cidr_block: 10.1.0.0/16

  aws_default_security_group:
    default:
      vpc_id: ${aws_vpc.mainvpc.id}
      ingress:
        protocol: -1
        self: true
        from_port: 0
        to_port: 0
      egress:
        from_port: 0
        to_port: 0
        protocol: -1
        cidr_blocks: 
          - 0.0.0.0/0```

## Example Config To Deny All Egress Traffic, Allowing Ingress

```yaml
resource:
  aws_vpc:
    mainvpc:
      cidr_block: 10.1.0.0/16

  aws_default_security_group:
    default:
      vpc_id: ${aws_vpc.mainvpc.id}
      ingress:
        protocol: -1
        self: true
        from_port: 0
        to_port: 0```

## Argument Reference

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `egress` - (Optional, VPC only) Configuration block. Detailed below.
* `ingress` - (Optional) Configuration block. Detailed below.
* `tags` - (Optional) Map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `vpc_id` - (Optional, Forces new resource) VPC ID. **Note that changing the `vpc_id` will _not_ restore any default security group rules that were modified, added, or removed.** It will be left in its current state.

### egress and ingress

Both arguments are processed in attribute-as-blocks mode.

Both `egress` and `ingress` objects have the same arguments.

* `cidr_blocks` - (Optional) List of CIDR blocks.
* `description` - (Optional) Description of this rule.
* `from_port` - (Required) Start port (or ICMP type number if protocol is `icmp`)
* `ipv6_cidr_blocks` - (Optional) List of IPv6 CIDR blocks.
* `prefix_list_ids` - (Optional) List of prefix list IDs (for allowing access to VPC endpoints)
* `protocol` - (Required) Protocol. If you select a protocol of "-1" (semantically equivalent to `all`, which is not a valid value here), you must specify a `from_port` and `to_port` equal to `0`. If not `icmp`, `tcp`, `udp`, or `-1` use the [protocol number](https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml).
* `security_groups` - (Optional) List of security groups. A group name can be used relative to the default VPC. Otherwise, group ID.
* `self` - (Optional) Whether the security group itself will be added as a source to this egress rule.
* `to_port` - (Required) End range port (or ICMP code if protocol is `icmp`).

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the security group.
* `description` - Description of the security group.
* `id` - ID of the security group.
* `name` - Name of the security group.
* `owner_id` - Owner ID.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

[aws-default-security-groups]: http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-network-security.html#default-security-group

## Import

```bash
ytofu import aws_default_security_group.default_sg sg-903004f8
```
