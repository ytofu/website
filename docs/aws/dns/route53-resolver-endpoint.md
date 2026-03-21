# Route53 Resolver Endpoint

Manage Route53 Resolver Endpoint resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_route53_resolver_endpoint:
    foo:
      name: foo
      direction: INBOUND
      resolver_endpoint_type: IPV4
      security_group_ids:
        - ${aws_security_group.sg1.id}
        - ${aws_security_group.sg2.id}
      ip_address:
        subnet_id: ${aws_subnet.sn1.id}
      ip_address:
        subnet_id: ${aws_subnet.sn2.id}
        ip: 10.0.64.4
      protocols: 
        - Do53
        - DoH
      tags:
        Environment: Prod
```
