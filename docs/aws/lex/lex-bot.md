# Lex Bot

Manage Lex Bot resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lex_bot:
    order_flowers_bot:
      abort_statement:
        message:
          content: Sorry, I am not able to assist at this time
          content_type: PlainText
      child_directed: false
      clarification_prompt:
        max_attempts: 2
        message:
          content: "I didn't understand you, what would you like to do?"
          content_type: PlainText
      create_version: false
      description: Bot to order flowers on the behalf of a user
      idle_session_ttl_in_seconds: 600
      intent:
        intent_name: OrderFlowers
        intent_version: 1
      locale: en-US
      name: OrderFlowers
      process_behavior: BUILD
      voice_id: Salli
```
