# Synthetics Group Association

Manage Synthetics Group Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_synthetics_group_association:
    example:
      group_name: ${aws_synthetics_group.example.name}
      canary_arn: ${aws_synthetics_canary.example.arn}
```
