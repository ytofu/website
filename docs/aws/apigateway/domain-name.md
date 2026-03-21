# API Gateway Domain Name

Configure custom domains using ytofu YAML.

## Regional Domain

```yaml
resource:
  aws_api_gateway_domain_name:
    example:
      domain_name: api.example.com
      regional_certificate_arn: ${aws_acm_certificate.example.arn}
      endpoint_configuration:
        types:
          - REGIONAL

  aws_api_gateway_base_path_mapping:
    example:
      api_id: ${aws_api_gateway_rest_api.example.id}
      stage_name: ${aws_api_gateway_stage.example.stage_name}
      domain_name: ${aws_api_gateway_domain_name.example.domain_name}
```

## Edge-Optimized Domain

```yaml
resource:
  aws_api_gateway_domain_name:
    example:
      certificate_arn: ${aws_acm_certificate.example.arn}
      domain_name: api.example.com
```
