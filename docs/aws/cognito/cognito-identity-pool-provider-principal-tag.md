# Cognito Identity Pool Provider Principal Tag

Manage Cognito Identity Pool Provider Principal Tag resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cognito_user_pool:
    example:
      name: user pool
      auto_verified_attributes: 
        - email

resource:
  aws_cognito_user_pool_client:
    example:
      name: client
      user_pool_id: ${aws_cognito_user_pool.example.id}
      supported_identity_providers: []
resource:
  aws_cognito_identity_pool:
    example:
      identity_pool_name: identity pool
      allow_unauthenticated_identities: false
      cognito_identity_providers:
        client_id: ${aws_cognito_user_pool_client.example.id}
        provider_name: ${aws_cognito_user_pool.example.endpoint}
        server_side_token_check: false

resource:
  aws_cognito_identity_pool_provider_principal_tag:
    example:
      identity_pool_id: ${aws_cognito_identity_pool.example.id}
      identity_provider_name: ${aws_cognito_user_pool.example.endpoint}
      use_defaults: false
      principal_tags:
        test: value
```
