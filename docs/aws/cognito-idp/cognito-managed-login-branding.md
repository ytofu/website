# Cognito Managed Login Branding

Manage Cognito Managed Login Branding resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cognito_managed_login_branding:
    client:
      client_id: ${aws_cognito_user_pool_client.example.id}
      user_pool_id: ${aws_cognito_user_pool.example.id}
      use_cognito_provided_values: true
```

## Custom Branding Style

```yaml
resource:
  aws_cognito_managed_login_branding:
    client:
      client_id: ${aws_cognito_user_pool_client.example.id}
      user_pool_id: ${aws_cognito_user_pool.example.id}
      asset:
        bytes: example-value
        category: PAGE_HEADER_BACKGROUND
        color_mode: DARK
        extension: SVG
      settings: '{ # Your settings here. }'
```
