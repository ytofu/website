# Sagemaker Workforce

Manage Sagemaker Workforce resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_workforce:
    example:
      workforce_name: example
      cognito_config:
        client_id: ${aws_cognito_user_pool_client.example.id}
        user_pool: ${aws_cognito_user_pool_domain.example.user_pool_id}

resource:
  aws_cognito_user_pool:
    example:
      name: example

resource:
  aws_cognito_user_pool_client:
    example:
      name: example
      generate_secret: true
      user_pool_id: ${aws_cognito_user_pool.example.id}

resource:
  aws_cognito_user_pool_domain:
    example:
      domain: example
      user_pool_id: ${aws_cognito_user_pool.example.id}
```

## Oidc Usage

```yaml
resource:
  aws_sagemaker_workforce:
    example:
      workforce_name: example
      oidc_config:
        authorization_endpoint: "https://example.com"
        client_id: example
        client_secret: example
        issuer: "https://example.com"
        jwks_uri: "https://example.com"
        logout_endpoint: "https://example.com"
        token_endpoint: "https://example.com"
        user_info_endpoint: "https://example.com"
```
