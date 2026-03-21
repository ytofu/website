# Connect Bot Association

Manage Connect Bot Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_connect_bot_association:
    example:
      instance_id: ${aws_connect_instance.example.id}
      lex_bot:
        lex_region: us-west-2
        name: Test
```

## Including a sample Lex bot

```yaml
data:
  aws_region:
    current:

resource:
  aws_lex_intent:
    example:
      create_version: true
      name: connect_lex_intent
      fulfillment_activity:
        type: ReturnIntent
      sample_utterances:
        - I would like to pick up flowers.

resource:
  aws_lex_bot:
    example:
      abort_statement:
        message:
          content: Sorry, I am not able to assist at this time.
          content_type: PlainText
      clarification_prompt:
        max_attempts: 2
        message:
          content: "I didn't understand you, what would you like to do?"
          content_type: PlainText
      intent:
        intent_name: ${aws_lex_intent.example.name}
        intent_version: 1
      child_directed: false
      name: connect_lex_bot
      process_behavior: BUILD

resource:
  aws_connect_bot_association:
    example:
      instance_id: ${aws_connect_instance.example.id}
      lex_bot:
        lex_region: ${data.aws_region.current.region}
        name: ${aws_lex_bot.example.name}
```
