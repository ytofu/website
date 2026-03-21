# Lexv2models Slot Type

Manage Lexv2models Slot Type resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lexv2models_bot:
    example:
      name: example
      idle_session_ttl_in_seconds: 60
      role_arn: ${aws_iam_role.example.arn}
      data_privacy:
        child_directed: true

resource:
  aws_lexv2models_bot_locale:
    example:
      locale_id: en_US
      bot_id: ${aws_lexv2models_bot.example.id}
      bot_version: DRAFT
      n_lu_intent_confidence_threshold: 0.7

resource:
  aws_lexv2models_bot_version:
    example:
      bot_id: ${aws_lexv2models_bot.example.id}
      locale_specification:
        source_bot_version: DRAFT

resource:
  aws_lexv2models_slot_type:
    example:
      bot_id: ${aws_lexv2models_bot.example.id}
      bot_version: ${aws_lexv2models_bot_locale.example.bot_version}
      name: example
      locale_id: ${aws_lexv2models_bot_locale.example.locale_id}
```

## value_selection_setting Usage

```yaml
resource:
  aws_lexv2models_slot_type:
    example:
      bot_id: ${aws_lexv2models_bot.example.id}
      bot_version: ${aws_lexv2models_bot_locale.example.bot_version}
      name: example
      locale_id: ${aws_lexv2models_bot_locale.example.locale_id}
      value_selection_setting:
        resolution_strategy: OriginalValue
        advanced_recognition_setting:
          audio_recognition_strategy: UseSlotValuesAsCustomVocabulary
      slot_type_values:
        sample_value:
          value: exampleValue
```
