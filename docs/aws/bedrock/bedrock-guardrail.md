# Bedrock Guardrail

Manage Bedrock Guardrail resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_bedrock_guardrail:
    example:
      name: example
      blocked_input_messaging: example
      blocked_outputs_messaging: example
      description: example
      content_policy_config:
        filters_config:
          input_strength: MEDIUM
          output_strength: MEDIUM
          type: HATE
        tier_config:
          tier_name: STANDARD
      sensitive_information_policy_config:
        pii_entities_config:
          action: BLOCK
          input_action: BLOCK
          output_action: ANONYMIZE
          input_enabled: true
          output_enabled: true
          type: NAME
        regexes_config:
          action: BLOCK
          input_action: BLOCK
          output_action: BLOCK
          input_enabled: true
          output_enabled: false
          description: example regex
          name: regex_example
          pattern: "^\\d{3}-\\d{2}-\\d{4}$"
      topic_policy_config:
        topics_config:
          name: investment_topic
          examples: 
            - Where should I invest my money ?
          type: DENY
          definition: Investment advice refers to inquiries, guidance, or recommendations regarding the management or allocation of funds or assets with the goal of generating returns .
        tier_config:
          tier_name: CLASSIC
      word_policy_config:
        managed_word_lists_config:
          type: PROFANITY
        words_config:
          text: HATE
```
