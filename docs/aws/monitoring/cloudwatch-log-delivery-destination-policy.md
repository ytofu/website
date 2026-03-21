# Cloudwatch Log Delivery Destination Policy

Manage Cloudwatch Log Delivery Destination Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudwatch_log_delivery_destination_policy:
    example:
      delivery_destination_name: ${aws_cloudwatch_log_delivery_destination.example.name}
      delivery_destination_policy: ${data.aws_iam_policy_document.example.json}
```
