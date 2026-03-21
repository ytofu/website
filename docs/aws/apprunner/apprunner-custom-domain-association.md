# Apprunner Custom Domain Association

Manage Apprunner Custom Domain Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_apprunner_custom_domain_association:
    example:
      domain_name: example.com
      service_arn: ${aws_apprunner_service.example.arn}
```
