# Devicefarm Network Profile

Manage Devicefarm Network Profile resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_devicefarm_project:
    example:
      name: example

resource:
  aws_devicefarm_network_profile:
    example:
      name: example
      project_arn: ${aws_devicefarm_project.example.arn}
```
