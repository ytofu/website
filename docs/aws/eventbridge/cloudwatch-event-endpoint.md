# Cloudwatch Event Endpoint

Manage Cloudwatch Event Endpoint resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudwatch_event_endpoint:
    this:
      name: global-endpoint
      role_arn: ${aws_iam_role.replication.arn}
      event_bus:
        event_bus_arn: ${aws_cloudwatch_event_bus.primary.arn}
      event_bus:
        event_bus_arn: ${aws_cloudwatch_event_bus.secondary.arn}
      replication_config:
        state: DISABLED
      routing_config:
        failover_config:
          primary:
            health_check: ${aws_route53_health_check.primary.arn}
          secondary:
            route: us-east-2
```
