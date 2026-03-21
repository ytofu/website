# Cognito User Pool Domain

Configure hosted UI domains for Cognito user pools using ytofu YAML.

## Cognito Prefix Domain

```yaml
resource:
  aws_cognito_user_pool_domain:
    main:
      domain: example-domain
      user_pool_id: ${aws_cognito_user_pool.example.id}
```

## Custom Domain

```yaml
resource:
  aws_cognito_user_pool_domain:
    main:
      domain: auth.example.com
      certificate_arn: ${aws_acm_certificate.cert.arn}
      user_pool_id: ${aws_cognito_user_pool.example.id}
```
