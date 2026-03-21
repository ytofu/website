# Lexv2models Slot

Manage Lexv2models Slot resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lexv2models_slot:
    example:
      bot_id: ${aws_lexv2models_bot.example.id}
      bot_version: ${aws_lexv2models_bot_version.example.bot_version}
      intent_id: ${aws_lexv2models_intent.example.id}
      locale_id: ${aws_lexv2models_bot_locale.example.locale_id}
      name: example
```

## `value_elicitation_setting` Example

```yaml
resource:
  aws_lexv2models_slot:
    example:
      bot_id: ${aws_lexv2models_bot.test.id}
      bot_version: ${aws_lexv2models_bot_locale.test.bot_version}
      intent_id: ${aws_lexv2models_intent.test.intent_id}
      locale_id: ${aws_lexv2models_bot_locale.test.locale_id}
      name: example
      value_elicitation_setting:
        slot_constraint: Required
        prompt_specification:
          allow_interrupt: true
          max_retries: 1
          message_selection_strategy: Random
          message_group:
            message:
              plain_text_message:
                value: What is your favorite color?
          prompt_attempts_specification:
            allow_interrupt: true
            map_block_key: Initial
            allowed_input_types:
              allow_audio_input: true
              allow_dtmf_input: true
            audio_and_dtmf_input_specification:
              start_timeout_ms: 4000
              audio_specification:
                end_timeout_ms: 640
                max_length_ms: 15000
              dtmf_specification:
                deletion_character: "*"
                end_character: "#"
                end_timeout_ms: 5000
                max_length: 513
            text_input_specification:
              start_timeout_ms: 30000
          prompt_attempts_specification:
            allow_interrupt: true
            map_block_key: Retry1
            allowed_input_types:
              allow_audio_input: true
              allow_dtmf_input: true
            audio_and_dtmf_input_specification:
              start_timeout_ms: 4000
              audio_specification:
                end_timeout_ms: 640
                max_length_ms: 15000
              dtmf_specification:
                deletion_character: "*"
                end_character: "#"
                end_timeout_ms: 5000
                max_length: 513
            text_input_specification:
              start_timeout_ms: 30000
```
