# Rekognition Project

Manage Rekognition Project resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_rekognition_project:
    example:
      name: example-project
      auto_update: ENABLED
      feature: CONTENT_MODERATION
```

## Custom Labels

```yaml
resource:
  aws_rekognition_project:
    example:
      name: example-project
      feature: CUSTOM_LABELS
```
