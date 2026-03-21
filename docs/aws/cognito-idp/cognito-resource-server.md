# Cognito Resource Server

Manage Cognito Resource Server resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cognito_user_pool:
    pool:
      name: pool

resource:
  aws_cognito_resource_server:
    resource:
      identifier: "https://example.com"
      name: example
      user_pool_id: ${aws_cognito_user_pool.pool.id}
```

## Create a resource server with sample-scope

```yaml
resource:
  aws_cognito_user_pool:
    pool:
      name: pool

resource:
  aws_cognito_resource_server:
    resource:
      identifier: "https://example.com"
      name: example
      scope:
        scope_name: sample-scope
        scope_description: a Sample Scope Description
      user_pool_id: ${aws_cognito_user_pool.pool.id}
```
