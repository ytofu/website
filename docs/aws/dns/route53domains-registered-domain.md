# Route53domains Registered Domain

Manage Route53domains Registered Domain resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_route53domains_registered_domain:
    example:
      domain_name: example.com
      name_server:
        name: ns-195.awsdns-24.com
      name_server:
        name: ns-874.awsdns-45.net
      tags:
        Environment: test
```
