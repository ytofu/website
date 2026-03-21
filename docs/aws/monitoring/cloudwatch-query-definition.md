# Cloudwatch Query Definition

Manage Cloudwatch Query Definition resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudwatch_query_definition:
    example:
      name: custom_query
      log_group_names:
        - /aws/logGroup1
        - /aws/logGroup2
      query_string: |
        fields @timestamp, @message
        | sort @timestamp desc
        | limit 25
```
