# API Gateway Domain Name

Manage API Gateway Domain Name resources using ytofu YAML.

## Edge Optimized (ACM Certificate)

```yaml
resource:
  aws_api_gateway_domain_name:
    example:
      certificate_arn: ${aws_acm_certificate_validation.example.certificate_arn}
      domain_name: api.example.com

resource:
  aws_route53_record:
    example:
      name: ${aws_api_gateway_domain_name.example.domain_name}
      type: A
      zone_id: ${aws_route53_zone.example.id}
      alias:
        evaluate_target_health: true
        name: ${aws_api_gateway_domain_name.example.cloudfront_domain_name}
        zone_id: ${aws_api_gateway_domain_name.example.cloudfront_zone_id}
```

## Edge Optimized (IAM Certificate)

```yaml
resource:
  aws_api_gateway_domain_name:
    example:
      domain_name: api.example.com
      certificate_name: example-api
      certificate_body: file-content
      certificate_chain: file-content
      certificate_private_key: file-content

resource:
  aws_route53_record:
    example:
      zone_id: ${aws_route53_zone.example.id}
      name: ${aws_api_gateway_domain_name.example.domain_name}
      type: A
      alias:
        name: ${aws_api_gateway_domain_name.example.cloudfront_domain_name}
        zone_id: ${aws_api_gateway_domain_name.example.cloudfront_zone_id}
        evaluate_target_health: true
```

## Regional (ACM Certificate)

```yaml
resource:
  aws_api_gateway_domain_name:
    example:
      domain_name: api.example.com
      regional_certificate_arn: ${aws_acm_certificate_validation.example.certificate_arn}
      endpoint_configuration:
        types: 
          - REGIONAL

resource:
  aws_route53_record:
    example:
      name: ${aws_api_gateway_domain_name.example.domain_name}
      type: A
      zone_id: ${aws_route53_zone.example.id}
      alias:
        evaluate_target_health: true
        name: ${aws_api_gateway_domain_name.example.regional_domain_name}
        zone_id: ${aws_api_gateway_domain_name.example.regional_zone_id}
```

## Regional (IAM Certificate)

```yaml
resource:
  aws_api_gateway_domain_name:
    example:
      certificate_body: file-content
      certificate_chain: file-content
      certificate_private_key: file-content
      domain_name: api.example.com
      regional_certificate_name: example-api
      endpoint_configuration:
        types: 
          - REGIONAL

resource:
  aws_route53_record:
    example:
      name: ${aws_api_gateway_domain_name.example.domain_name}
      type: A
      zone_id: ${aws_route53_zone.example.id}
      alias:
        evaluate_target_health: true
        name: ${aws_api_gateway_domain_name.example.regional_domain_name}
        zone_id: ${aws_api_gateway_domain_name.example.regional_zone_id}
```

## Enhanced Security Policy

```yaml
resource:
  aws_api_gateway_domain_name:
    example:
      domain_name: api.example.com
      regional_certificate_arn: ${aws_acm_certificate_validation.example.certificate_arn}
      security_policy: SecurityPolicy_TLS13_1_3_2025_09
      endpoint_access_mode: STRICT
      endpoint_configuration:
        types: 
          - REGIONAL
```
