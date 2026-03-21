# SNS Topic Data Protection Policy

Manage SNS Topic Data Protection Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sns_topic:
    example:
      name: example

resource:
  aws_sns_topic_data_protection_policy:
    example:
      arn: ${aws_sns_topic.example.arn}
      policy: 'example-json-policy'
```
