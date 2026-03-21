# Cloudwatch Log Delivery Source

Manage Cloudwatch Log Delivery Source resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudwatch_log_delivery_source:
    example:
      name: example
      log_type: APPLICATION_LOGS
      resource_arn: ${aws_bedrockagent_knowledge_base.example.arn}
```
