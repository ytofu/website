# AppSync Domain Name

Configure custom domains for AppSync APIs using ytofu YAML.

## Basic Domain

```yaml
resource:
  aws_appsync_domain_name:
    example:
      domain_name: api.example.com
      certificate_arn: ${aws_acm_certificate.example.arn}

  aws_appsync_domain_name_api_association:
    example:
      api_id: ${aws_appsync_graphql_api.example.id}
      domain_name: ${aws_appsync_domain_name.example.domain_name}
```
