# Lexv2models Bot Version

Manage Lexv2models Bot Version resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lexv2models_bot_version:
    test:
      bot_id: ${aws_lexv2models_bot.test.id}
      locale_specification:
        source_bot_version: DRAFT
```
