# Cognito User Pool Ui Customization

Manage Cognito User Pool Ui Customization resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cognito_user_pool:
    example:
      name: example

resource:
  aws_cognito_user_pool_domain:
    example:
      domain: example
      user_pool_id: ${aws_cognito_user_pool.example.id}

resource:
  aws_cognito_user_pool_client:
    example:
      name: example
      user_pool_id: ${aws_cognito_user_pool.example.id}

resource:
  aws_cognito_user_pool_ui_customization:
    example:
      client_id: ${aws_cognito_user_pool_client.example.id}
      css: ".label-customizable {font-weight: 400;}"
      image_file: ${filebase64("logo.png")}
      user_pool_id: ${aws_cognito_user_pool_domain.example.user_pool_id}
```

## UI customization settings for all clients

```yaml
resource:
  aws_cognito_user_pool:
    example:
      name: example

resource:
  aws_cognito_user_pool_domain:
    example:
      domain: example
      user_pool_id: ${aws_cognito_user_pool.example.id}

resource:
  aws_cognito_user_pool_ui_customization:
    example:
      css: ".label-customizable {font-weight: 400;}"
      image_file: ${filebase64("logo.png")}
      user_pool_id: ${aws_cognito_user_pool_domain.example.user_pool_id}
```
