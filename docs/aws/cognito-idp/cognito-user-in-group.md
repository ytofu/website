# Cognito User In Group

Manage Cognito User In Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cognito_user_pool:
    example:
      name: example
      password_policy:
        temporary_password_validity_days: 7
        minimum_length: 6
        require_uppercase: false
        require_symbols: false
        require_numbers: false

resource:
  aws_cognito_user:
    example:
      user_pool_id: ${aws_cognito_user_pool.example.id}
      username: example

resource:
  aws_cognito_user_group:
    example:
      user_pool_id: ${aws_cognito_user_pool.example.id}
      name: example

resource:
  aws_cognito_user_in_group:
    example:
      user_pool_id: ${aws_cognito_user_pool.example.id}
      group_name: ${aws_cognito_user_group.example.name}
      username: ${aws_cognito_user.example.username}
```
