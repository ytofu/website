# Cognito Resource Server

Create OAuth resource servers using ytofu YAML.

## Basic Resource Server

```yaml
resource:
  aws_cognito_resource_server:
    resource:
      identifier: https://example.com
      name: example
      user_pool_id: ${aws_cognito_user_pool.pool.id}
```

## With Scopes

```yaml
resource:
  aws_cognito_resource_server:
    resource:
      identifier: https://api.example.com
      name: api
      user_pool_id: ${aws_cognito_user_pool.pool.id}
      scope:
        - scope_name: read
          scope_description: Read access
        - scope_name: write
          scope_description: Write access
```
