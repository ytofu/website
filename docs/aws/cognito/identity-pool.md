# Cognito Identity Pool

Create federated identity pools using ytofu YAML.

## Basic Identity Pool

```yaml
resource:
  aws_cognito_identity_pool:
    main:
      identity_pool_name: identity pool
      allow_unauthenticated_identities: false
```

## With Cognito User Pool Provider

```yaml
resource:
  aws_cognito_identity_pool:
    main:
      identity_pool_name: identity pool
      allow_unauthenticated_identities: false
      cognito_identity_providers:
        - client_id: ${aws_cognito_user_pool_client.client.id}
          provider_name: ${aws_cognito_user_pool.pool.endpoint}
          server_side_token_check: false
```

## With Social Providers

```yaml
resource:
  aws_cognito_identity_pool:
    main:
      identity_pool_name: identity pool
      allow_unauthenticated_identities: false
      supported_login_providers:
        graph.facebook.com: "7346241598935552"
        accounts.google.com: 123456789012.apps.googleusercontent.com
```

## With Role Attachment

```yaml
resource:
  aws_cognito_identity_pool_roles_attachment:
    main:
      identity_pool_id: ${aws_cognito_identity_pool.main.id}
      roles:
        authenticated: ${aws_iam_role.authenticated.arn}
        unauthenticated: ${aws_iam_role.unauthenticated.arn}
```
