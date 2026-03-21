# Route53 Delegation Set

Manage Route53 Delegation Set resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_route53_delegation_set:
    main:
      reference_name: DynDNS

resource:
  aws_route53_zone:
    primary:
      name: hashicorp.com
      delegation_set_id: ${aws_route53_delegation_set.main.id}

resource:
  aws_route53_zone:
    secondary:
      name: terraform.io
      delegation_set_id: ${aws_route53_delegation_set.main.id}
```
