# API Gateway v2 Domain Name

Configure custom domains for HTTP APIs using ytofu YAML.

## Basic Domain

```yaml
resource:
  aws_apigatewayv2_domain_name:
    example:
      domain_name: api.example.com
      domain_name_configuration:
        certificate_arn: ${aws_acm_certificate.example.arn}
        endpoint_type: REGIONAL
        security_policy: TLS_1_2

  aws_apigatewayv2_api_mapping:
    example:
      api_id: ${aws_apigatewayv2_api.example.id}
      domain_name: ${aws_apigatewayv2_domain_name.example.id}
      stage: ${aws_apigatewayv2_stage.example.id}
```
