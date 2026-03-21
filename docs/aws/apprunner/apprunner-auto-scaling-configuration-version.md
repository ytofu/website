# Apprunner Auto Scaling Configuration Version

Manage Apprunner Auto Scaling Configuration Version resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_apprunner_auto_scaling_configuration_version:
    example:
      auto_scaling_configuration_name: example
      max_concurrency: 50
      max_size: 10
      min_size: 2
      tags:
        Name: example-apprunner-autoscaling
```
