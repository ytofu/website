# App Runner Custom Domain

Configure custom domains for App Runner services using ytofu YAML.

## Basic Domain

```yaml
resource:
  aws_apprunner_custom_domain_association:
    example:
      domain_name: app.example.com
      service_arn: ${aws_apprunner_service.example.arn}
```
