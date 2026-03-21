# Apprunner Observability Configuration

Manage Apprunner Observability Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_apprunner_observability_configuration:
    example:
      observability_configuration_name: example
      trace_configuration:
        vendor: AWSXRAY
      tags:
        Name: example-apprunner-observability-configuration
```
