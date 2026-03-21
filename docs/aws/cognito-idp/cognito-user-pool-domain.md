# Cognito User Pool Domain

Manage Cognito User Pool Domain resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cognito_user_pool_domain:
    main:
      domain: example-domain
      user_pool_id: ${aws_cognito_user_pool.example.id}

resource:
  aws_cognito_user_pool:
    example:
      name: example-pool
```

## Custom Cognito domain

```yaml
resource:
  aws_cognito_user_pool_domain:
    main:
      domain: auth.example.com
      certificate_arn: ${aws_acm_certificate.cert.arn}
      user_pool_id: ${aws_cognito_user_pool.example.id}

resource:
  aws_cognito_user_pool:
    example:
      name: example-pool

data:
  aws_route53_zone:
    example:
      name: example.com

resource:
  aws_route53_record:
    auth-cognito-A:
      name: ${aws_cognito_user_pool_domain.main.domain}
      type: A
      zone_id: ${data.aws_route53_zone.example.zone_id}
      alias:
        evaluate_target_health: false
        name: ${aws_cognito_user_pool_domain.main.cloudfront_distribution}
        zone_id: ${aws_cognito_user_pool_domain.main.cloudfront_distribution_zone_id}
```
