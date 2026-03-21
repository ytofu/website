# VPC Security Group Rules Exclusive

Manage VPC Security Group Rules Exclusive resources using ytofu YAML.

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
