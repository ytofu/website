# Cognito User Pool Client

Create app clients for Cognito user pools using ytofu YAML.

## Basic Client

```yaml
resource:
  aws_cognito_user_pool_client:
    client:
      name: client
      user_pool_id: ${aws_cognito_user_pool.pool.id}
```

## With OAuth Flows

```yaml
resource:
  aws_cognito_user_pool_client:
    client:
      name: client
      user_pool_id: ${aws_cognito_user_pool.pool.id}
      generate_secret: true
      explicit_auth_flows:
        - ALLOW_REFRESH_TOKEN_AUTH
        - ALLOW_USER_SRP_AUTH
      allowed_oauth_flows:
        - code
        - implicit
      allowed_oauth_flows_user_pool_client: true
      allowed_oauth_scopes:
        - openid
        - email
        - profile
      callback_urls:
        - https://example.com/callback
      logout_urls:
        - https://example.com/logout
      supported_identity_providers:
        - COGNITO
```

## M2M Client (Client Credentials)

```yaml
resource:
  aws_cognito_user_pool_client:
    m2m:
      name: m2m-client
      user_pool_id: ${aws_cognito_user_pool.pool.id}
      generate_secret: true
      explicit_auth_flows:
        - ALLOW_REFRESH_TOKEN_AUTH
      allowed_oauth_flows:
        - client_credentials
      allowed_oauth_flows_user_pool_client: true
      allowed_oauth_scopes:
        - ${aws_cognito_resource_server.example.scope_identifiers[0]}
      supported_identity_providers:
        - COGNITO
```
