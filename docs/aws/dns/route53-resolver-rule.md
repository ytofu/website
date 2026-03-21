# Route53 Resolver Rule

Manage Route53 Resolver Rule resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_route53_resolver_rule:
    sys:
      domain_name: subdomain.example.com
      rule_type: SYSTEM
```

## Forward rule

```yaml
resource:
  aws_route53_resolver_rule:
    fwd:
      domain_name: example.com
      name: example
      rule_type: FORWARD
      resolver_endpoint_id: ${aws_route53_resolver_endpoint.foo.id}
      target_ip:
        ip: 123.45.67.89
      tags:
        Environment: Prod
```

## IPv6 Forward rule

```yaml
resource:
  aws_route53_resolver_rule:
    fwd:
      domain_name: example.com
      name: example
      rule_type: FORWARD
      resolver_endpoint_id: ${aws_route53_resolver_endpoint.foo.id}
      target_ip:
        ipv6: "2600:1f18:1686:2000:4e60:6e3e:258:da36"
      tags:
        Environment: Prod
```
