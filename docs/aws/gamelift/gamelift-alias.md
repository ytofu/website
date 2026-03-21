# Gamelift Alias

Manage Gamelift Alias resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_gamelift_alias:
    example:
      name: example-alias
      description: Example Description
      routing_strategy:
        message: Example Message
        type: TERMINAL
```
