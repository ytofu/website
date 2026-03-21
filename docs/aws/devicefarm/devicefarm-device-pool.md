# Devicefarm Device Pool

Manage Devicefarm Device Pool resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_devicefarm_device_pool:
    example:
      name: example
      project_arn: ${aws_devicefarm_project.example.arn}
      rule:
        attribute: OS_VERSION
        operator: EQUALS
        value: \"AVAILABLE\"
```
