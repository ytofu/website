# Route53 Resolver Dnssec Config

Manage Route53 Resolver Dnssec Config resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc:
    example:
      cidr_block: 10.0.0.0/16
      enable_dns_support: true
      enable_dns_hostnames: true

resource:
  aws_route53_resolver_dnssec_config:
    example:
      resource_id: ${aws_vpc.example.id}
```
