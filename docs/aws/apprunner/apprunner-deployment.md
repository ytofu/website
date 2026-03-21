# Apprunner Deployment

Manage Apprunner Deployment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_apprunner_deployment:
    example:
      service_arn: ${aws_apprunner_service.example.arn}
```
