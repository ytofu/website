# IOT Authorizer

Manage IOT Authorizer resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iot_authorizer:
    example:
      name: example
      authorizer_function_arn: ${aws_lambda_function.example.arn}
      signing_disabled: false
      status: ACTIVE
      token_key_name: Token-Header
      token_signing_public_keys:
        Key1: file-content
      tags:
        Name: example
```
