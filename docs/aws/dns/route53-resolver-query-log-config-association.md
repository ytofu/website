# Route53 Resolver Query Log Config Association

Manage Route53 Resolver Query Log Config Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_route53_resolver_query_log_config_association:
    example:
      resolver_query_log_config_id: ${aws_route53_resolver_query_log_config.example.id}
      resource_id: ${aws_vpc.example.id}
```
