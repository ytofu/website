# Evidently Segment

Manage Evidently Segment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_evidently_segment:
    example:
      name: example
      pattern: "{\"Price\":[{\"numeric\":[\">\",10,\"<=\",20]}]}"
      tags: 
```

## With JSON object in pattern

```yaml
resource:
  aws_evidently_segment:
    example:
      name: example
      pattern: |
        {
        "Price": [
        {
        "numeric": [">",10,"<=",20]
        }
        ]
        }
      tags: 
```

## With Description

```yaml
resource:
  aws_evidently_segment:
    example:
      name: example
      pattern: "{\"Price\":[{\"numeric\":[\">\",10,\"<=\",20]}]}"
      description: example
```
