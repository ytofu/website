# Resource: aws_default_network_acl

Provides a resource to manage a VPC's default network ACL. This resource can manage the default network ACL of the default or a non-default VPC.

## Basic Example

```yaml
resource:
  aws_vpc:
    mainvpc:
      cidr_block: 10.1.0.0/16

  aws_default_network_acl:
    default:
      default_network_acl_id: ${aws_vpc.mainvpc.default_network_acl_id}
      ingress:
        protocol: -1
        rule_no: 100
        action: allow
        cidr_block: 0.0.0.0/0
        from_port: 0
        to_port: 0
      egress:
        protocol: -1
        rule_no: 100
        action: allow
        cidr_block: 0.0.0.0/0
        from_port: 0
        to_port: 0```

## Example: Deny All Egress Traffic, Allow Ingress

```yaml
resource:
  aws_vpc:
    mainvpc:
      cidr_block: 10.1.0.0/16

  aws_default_network_acl:
    default:
      default_network_acl_id: ${aws_vpc.mainvpc.default_network_acl_id}
      ingress:
        protocol: -1
        rule_no: 100
        action: allow
        cidr_block: ${aws_default_vpc.mainvpc.cidr_block}
        from_port: 0
        to_port: 0```

## Example: Deny All Traffic To Any Subnet In The Default Network ACL

```yaml
resource:
  aws_vpc:
    mainvpc:
      cidr_block: 10.1.0.0/16

  aws_default_network_acl:
    default:
      default_network_acl_id: ${aws_vpc.mainvpc.default_network_acl_id}```

## Managing Subnets In A Default Network ACL

```yaml
resource:
  aws_default_network_acl:
    default:
      lifecycle:
        ignore_changes: 
          - subnet_ids
```

## Argument Reference

The following arguments are required:

* `default_network_acl_id` - (Required) Network ACL ID to manage. This attribute is exported from `aws_vpc`, or manually found via the AWS Console.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `egress` - (Optional) Configuration block for an egress rule. Detailed below.
* `ingress` - (Optional) Configuration block for an ingress rule. Detailed below.
* `subnet_ids` - (Optional) List of Subnet IDs to apply the ACL to. See the notes above on Managing Subnets in the Default Network ACL
* `tags` - (Optional) Map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### egress and ingress

Both the `egress` and `ingress` configuration blocks have the same arguments.

The following arguments are required:

* `action` - (Required) The action to take.
* `from_port` - (Required) The from port to match.
* `protocol` - (Required) The protocol to match. If using the -1 'all' protocol, you must specify a from and to port of 0.
* `rule_no` - (Required) The rule number. Used for ordering.
* `to_port` - (Required) The to port to match.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `cidr_block` - (Optional) The CIDR block to match. This must be a valid network mask.
* `icmp_code` - (Optional) The ICMP type code to be used. Default 0.
* `icmp_type` - (Optional) The ICMP type to be used. Default 0.
* `ipv6_cidr_block` - (Optional) The IPv6 CIDR block.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Default Network ACL
* `id` - ID of the Default Network ACL
* `owner_id` - ID of the AWS account that owns the Default Network ACL
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
* `vpc_id` -  ID of the associated VPC

[aws-network-acls]: http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_ACLs.html

## Import

```bash
ytofu import aws_default_network_acl.sample acl-7aaabd18
```
