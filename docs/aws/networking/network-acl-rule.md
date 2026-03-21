# Resource: aws_network_acl_rule

Creates an entry (a rule) in a network ACL with the specified rule number.

## Basic Example

```yaml
resource:
  aws_network_acl:
    bar:
      vpc_id: ${aws_vpc.foo.id}

  aws_network_acl_rule:
    bar:
      network_acl_id: ${aws_network_acl.bar.id}
      rule_number: 200
      egress: false
      protocol: tcp
      rule_action: allow
      cidr_block: ${aws_vpc.foo.cidr_block}
      from_port: 22
      to_port: 22```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `network_acl_id` - (Required) The ID of the network ACL.
* `rule_number` - (Required) The rule number for the entry (for example, 100). ACL entries are processed in ascending order by rule number.
* `egress` - (Optional, bool) Indicates whether this is an egress rule (rule is applied to traffic leaving the subnet). Default `false`.
* `protocol` - (Required) The protocol. A value of -1 means all protocols.
* `rule_action` - (Required) Indicates whether to allow or deny the traffic that matches the rule. Accepted values: `allow` | `deny`
* `cidr_block` - (Optional) The network range to allow or deny, in CIDR notation (for example 172.16.0.0/24 ).
* `ipv6_cidr_block` - (Optional) The IPv6 CIDR block to allow or deny.
* `from_port` - (Optional) The from port to match.
* `to_port` - (Optional) The to port to match.
* `icmp_type` - (Optional) ICMP protocol: The ICMP type. Required if specifying ICMP for the protocolE.g., -1
* `icmp_code` - (Optional) ICMP protocol: The ICMP code. Required if specifying ICMP for the protocolE.g., -1

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the network ACL Rule

## Import

```bash
ytofu import aws_network_acl_rule.my_rule acl-7aaabd18:100:tcp:false
```
