# Cloudwatch Log Transformer

Manage Cloudwatch Log Transformer resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudwatch_log_transformer:
    example:
      log_group_arn: ${aws_cloudwatch_log_group.example.arn}
      transformer_config:
        parse_json:

resource:
  aws_cloudwatch_log_group:
    example:
      name: example
```
