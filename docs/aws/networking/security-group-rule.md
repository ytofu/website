# Resource: aws_security_group_rule

Provides a security group rule resource. Represents a single `ingress` or `egress` group rule, which can be added to external Security Groups.

## Basic Example

```yaml
resource:
  aws_security_group_rule:
    example:
      type: ingress
      from_port: 0
      to_port: 65535
      protocol: tcp
      cidr_blocks: 
        - ${aws_vpc.example.cidr_block}
      ipv6_cidr_blocks: 
        - ${aws_vpc.example.ipv6_cidr_block}
      security_group_id: sg-123456
```

## Usage With Prefix List IDs

```yaml
resource:
  aws_security_group_rule:
    allow_all:
      type: egress
      to_port: 0
      protocol: -1
      prefix_list_ids: 
        - ${aws_vpc_endpoint.my_endpoint.prefix_list_id}
      from_port: 0
      security_group_id: sg-123456

  aws_vpc_endpoint:
    my_endpoint:```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `from_port` - (Required) Start port (or ICMP type number if protocol is "icmp" or "icmpv6").
* `protocol` - (Required) Protocol. If not icmp, icmpv6, tcp, udp, or all use the [protocol number](https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml)
* `security_group_id` - (Required) Security group to apply this rule to.
* `to_port` - (Required) End port (or ICMP code if protocol is "icmp").
* `type` - (Required) Type of rule being created. Valid options are `ingress` (inbound)
or `egress` (outbound).

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

* `cidr_blocks` - (Optional) List of CIDR blocks. Cannot be specified with `source_security_group_id` or `self`.
* `description` - (Optional) Description of the rule.
* `ipv6_cidr_blocks` - (Optional) List of IPv6 CIDR blocks. Cannot be specified with `source_security_group_id` or `self`.
* `prefix_list_ids` - (Optional) List of Prefix List IDs.
* `self` - (Optional) Whether the security group itself will be added as a source to this ingress rule. Cannot be specified with `cidr_blocks`, `ipv6_cidr_blocks`, or `source_security_group_id`.
* `source_security_group_id` - (Optional) Security group id to allow access to/from, depending on the `type`. Cannot be specified with `cidr_blocks`, `ipv6_cidr_blocks`, or `self`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - ID of the security group rule.
* `security_group_rule_id` - If the `aws_security_group_rule` resource has a single source or destination then this is the AWS Security Group Rule resource ID. Otherwise it is empty.

## Timeouts

Configuration options:

- `create` - (Default `5m`)

## Import

```bash
ytofu import aws_security_group_rule.ingress sg-6e616f6d69_ingress_tcp_8000_8000_10.0.3.0/24
```
