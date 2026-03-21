# VPC Security Group Egress Rule

Manage VPC Security Group Egress Rule resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc_security_group_egress_rule:
    example:
      security_group_id: ${aws_security_group.example.id}
      cidr_ipv4: 10.0.0.0/8
      from_port: 80
      ip_protocol: tcp
      to_port: 80
```
