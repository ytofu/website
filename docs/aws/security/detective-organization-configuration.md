# Detective Organization Configuration

Manage Detective Organization Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_detective_graph:
    example:
      enable: true

resource:
  aws_detective_organization_configuration:
    example:
      auto_enable: true
      graph_arn: ${aws_detective_graph.example.graph_arn}
```
