# Resource: aws_vpc_security_group_ingress_rule

Manages an inbound (ingress) rule for a security group.

## Basic Example

```yaml
resource:
  aws_security_group:
    example:
      name: example
      description: example
      vpc_id: ${aws_vpc.main.id}
      tags:
        Name: example

  aws_vpc_security_group_ingress_rule:
    example:
      security_group_id: ${aws_security_group.example.id}
      cidr_ipv4: 10.0.0.0/8
      from_port: 80
      ip_protocol: tcp
      to_port: 80```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `cidr_ipv4` - (Optional) The source IPv4 CIDR range.
* `cidr_ipv6` - (Optional) The source IPv6 CIDR range.
* `description` - (Optional) The security group rule description.
* `from_port` - (Optional) The start of port range for the TCP and UDP protocols, or an ICMP/ICMPv6 type.
* `ip_protocol` - (Required) The IP protocol name or number. Use `-1` to specify all protocols. Note that if `ip_protocol` is set to `-1`, it translates to all protocols, all port ranges, and `from_port` and `to_port` values should not be defined.
* `prefix_list_id` - (Optional) The ID of the source prefix list.
* `referenced_security_group_id` - (Optional) The source security group that is referenced in the rule.
* `security_group_id` - (Required) The ID of the security group.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `to_port` - (Optional) The end of port range for the TCP and UDP protocols, or an ICMP/ICMPv6 code.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The Amazon Resource Name (ARN) of the security group rule.
* `security_group_rule_id` - The ID of the security group rule.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_vpc_security_group_ingress_rule.example sgr-02108b27edd666983
```
