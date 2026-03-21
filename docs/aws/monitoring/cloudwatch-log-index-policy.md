# Cloudwatch Log Index Policy

Manage Cloudwatch Log Index Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudwatch_log_group:
    example:
      name: example

resource:
  aws_cloudwatch_log_index_policy:
    example:
      log_group_name: ${aws_cloudwatch_log_group.example.name}
      policy_document: '{ "Fields": ["eventName"] }'
```
