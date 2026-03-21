# Resource: aws_vpc_security_group_rules_exclusive

ytofu resource for managing an exclusive set of AWS VPC (Virtual Private Cloud) Security Group Rules.

## Basic Example

```yaml
resource:
  aws_vpc:
    example:
      cidr_block: 10.0.0.0/16

resource:
  aws_security_group:
    example:
      name: example
      vpc_id: ${aws_vpc.example.id}

resource:
  aws_vpc_security_group_ingress_rule:
    example:
      security_group_id: ${aws_security_group.example.id}
      cidr_ipv4: 10.0.0.0/8
      from_port: 80
      to_port: 80
      ip_protocol: tcp

resource:
  aws_vpc_security_group_egress_rule:
    example:
      security_group_id: ${aws_security_group.example.id}
      cidr_ipv4: 0.0.0.0/0
      ip_protocol: -1

resource:
  aws_vpc_security_group_rules_exclusive:
    example:
      security_group_id: ${aws_security_group.example.id}
      ingress_rule_ids: 
        - ${aws_vpc_security_group_ingress_rule.example.id}
      egress_rule_ids: 
        - ${aws_vpc_security_group_egress_rule.example.id}
```

## Disallow All Rules

```yaml
resource:
  aws_vpc_security_group_rules_exclusive:
    example:
      security_group_id: ${aws_security_group.example.id}
      ingress_rule_ids: []
      egress_rule_ids: []
```

## Argument Reference

This resource supports the following arguments:

* `egress_rule_ids` - (Required) Egress rule IDs.
* `ingress_rule_ids` - (Required) Ingress rule IDs.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `security_group_id` - (Required, Forces new resource) ID of the security group.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_vpc_security_group_rules_exclusive.example sg-1234567890abcdef0
```
