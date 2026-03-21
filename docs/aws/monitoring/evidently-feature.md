# Evidently Feature

Manage Evidently Feature resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_evidently_feature:
    example:
      name: example
      project: ${aws_evidently_project.example.name}
      description: example description
      variations:
        name: Variation1
        value:
          string_value: example
      tags: 
```

## With default variation

```yaml
resource:
  aws_evidently_feature:
    example:
      name: example
      project: ${aws_evidently_project.example.name}
      default_variation: Variation2
      variations:
        name: Variation1
        value:
          string_value: exampleval1
      variations:
        name: Variation2
        value:
          string_value: exampleval2
```

## With entity overrides

```yaml
resource:
  aws_evidently_feature:
    example:
      name: example
      project: ${aws_evidently_project.example.name}
      entity_overrides:
        test1: Variation1
      variations:
        name: Variation1
        value:
          string_value: exampleval1
      variations:
        name: Variation2
        value:
          string_value: exampleval2
```

## With evaluation strategy

```yaml
resource:
  aws_evidently_feature:
    example:
      name: example
      project: ${aws_evidently_project.example.name}
      evaluation_strategy: ALL_RULES
      entity_overrides:
        test1: Variation1
      variations:
        name: Variation1
        value:
          string_value: exampleval1
```
