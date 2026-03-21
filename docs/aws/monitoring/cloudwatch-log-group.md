# Cloudwatch Log Group

Manage Cloudwatch Log Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudwatch_log_group:
    yada:
      name: Yada
      tags:
        Environment: production
        Application: serviceA
```
