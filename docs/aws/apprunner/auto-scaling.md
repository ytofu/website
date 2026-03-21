# App Runner Auto Scaling

Configure auto scaling for App Runner services using ytofu YAML.

## Basic Config

```yaml
resource:
  aws_apprunner_auto_scaling_configuration_version:
    example:
      auto_scaling_configuration_name: example
      max_concurrency: 100
      max_size: 5
      min_size: 1
```
