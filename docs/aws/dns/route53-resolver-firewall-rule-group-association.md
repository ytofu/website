# Route53 Resolver Firewall Rule Group Association

Manage Route53 Resolver Firewall Rule Group Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_route53_resolver_firewall_rule_group:
    example:
      name: example

resource:
  aws_route53_resolver_firewall_rule_group_association:
    example:
      name: example
      firewall_rule_group_id: ${aws_route53_resolver_firewall_rule_group.example.id}
      priority: 100
      vpc_id: ${aws_vpc.example.id}
```
