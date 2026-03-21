# Lexv2models Bot Locale

Manage Lexv2models Bot Locale resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lexv2models_bot_locale:
    example:
      bot_id: ${aws_lexv2models_bot.example.id}
      bot_version: DRAFT
      locale_id: en_US
      n_lu_intent_confidence_threshold: 0.70
```

## Voice Settings

```yaml
resource:
  aws_lexv2models_bot_locale:
    example:
      bot_id: ${aws_lexv2models_bot.example.id}
      bot_version: DRAFT
      locale_id: en_US
      n_lu_intent_confidence_threshold: 0.70
      voice_settings:
        voice_id: Kendra
        engine: standard
```
