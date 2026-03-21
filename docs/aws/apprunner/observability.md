# App Runner Observability

Configure X-Ray tracing for App Runner services using ytofu YAML.

## Enable Tracing

```yaml
resource:
  aws_apprunner_observability_configuration:
    example:
      observability_configuration_name: example
      trace_configuration:
        vendor: AWSXRAY
```
