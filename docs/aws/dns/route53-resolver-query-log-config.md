# Route53 Resolver Query Log Config

Manage Route53 Resolver Query Log Config resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_route53_resolver_query_log_config:
    example:
      name: example
      destination_arn: ${aws_s3_bucket.example.arn}
      tags:
        Environment: Prod
```
