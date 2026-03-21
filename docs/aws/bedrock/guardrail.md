# Bedrock Guardrail

Create content guardrails for Bedrock using ytofu YAML.

## Basic Guardrail

```yaml
resource:
  aws_bedrock_guardrail:
    example:
      name: example
      blocked_input_messaging: I can't answer that.
      blocked_outputs_messaging: Response blocked.
      description: Example guardrail
      content_policy_config:
        filters_config:
          - input_strength: HIGH
            output_strength: HIGH
            type: HATE
          - input_strength: HIGH
            output_strength: HIGH
            type: VIOLENCE
          - input_strength: HIGH
            output_strength: HIGH
            type: SEXUAL
```
