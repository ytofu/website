# Cloudwatch Event Archive

Manage Cloudwatch Event Archive resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudwatch_event_bus:
    order:
      name: orders

resource:
  aws_cloudwatch_event_archive:
    order:
      name: order-archive
      event_source_arn: ${aws_cloudwatch_event_bus.order.arn}
```
