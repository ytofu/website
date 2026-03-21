# Route53 Resolver Rule Association

Manage Route53 Resolver Rule Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_route53_resolver_rule_association:
    example:
      resolver_rule_id: ${aws_route53_resolver_rule.sys.id}
      vpc_id: ${aws_vpc.foo.id}
```
