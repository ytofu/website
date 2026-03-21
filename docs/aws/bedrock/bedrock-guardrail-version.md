# Bedrock Guardrail Version

Manage Bedrock Guardrail Version resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_bedrock_guardrail_version:
    example:
      description: example
      guardrail_arn: ${aws_bedrock_guardrail.test.guardrail_arn}
      skip_destroy: true
```
