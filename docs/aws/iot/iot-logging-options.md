# IOT Logging Options

Manage IOT Logging Options resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iot_logging_options:
    example:
      default_log_level: WARN
      role_arn: ${aws_iam_role.example.arn}
```
