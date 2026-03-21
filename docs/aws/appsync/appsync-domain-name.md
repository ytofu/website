# Appsync Domain Name

Manage Appsync Domain Name resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appsync_domain_name:
    example:
      domain_name: api.example.com
      certificate_arn: ${aws_acm_certificate.example.arn}
```
