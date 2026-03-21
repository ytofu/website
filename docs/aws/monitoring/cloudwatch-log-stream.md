# Cloudwatch Log Stream

Manage Cloudwatch Log Stream resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudwatch_log_group:
    yada:
      name: Yada

resource:
  aws_cloudwatch_log_stream:
    foo:
      name: SampleLogStream1234
      log_group_name: ${aws_cloudwatch_log_group.yada.name}
```
