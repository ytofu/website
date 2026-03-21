# Resource: aws_route53_resolver_query_log_config_association

Provides a Route 53 Resolver query logging configuration association resource.

## Basic Example

```yaml
resource:
  aws_route53_resolver_query_log_config_association:
    example:
      resolver_query_log_config_id: ${aws_route53_resolver_query_log_config.example.id}
      resource_id: ${aws_vpc.example.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `resolver_query_log_config_id` - (Required) The ID of the [Route 53 Resolver query logging configuration](route53_resolver_query_log_config.html) that you want to associate a VPC with.
* `resource_id` - (Required) The ID of a VPC that you want this query logging configuration to log queries for.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` -The ID of the Route 53 Resolver query logging configuration association.

## Import

```bash
ytofu import aws_route53_resolver_query_log_config_association.example rqlca-b320624fef3c4d70
```
