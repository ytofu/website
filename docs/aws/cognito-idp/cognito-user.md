# Cognito User

Manage Cognito User resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cognito_user_pool:
    example:
      name: MyExamplePool

resource:
  aws_cognito_user:
    example:
      user_pool_id: ${aws_cognito_user_pool.example.id}
      username: example
```

## Setting user attributes

```yaml
resource:
  aws_cognito_user_pool:
    example:
      name: mypool
      schema:
        name: terraform
        attribute_data_type: Boolean
        mutable: false
        required: false
        developer_only_attribute: false
      schema:
        name: foo
        attribute_data_type: String
        mutable: false
        required: false
        developer_only_attribute: false
        string_attribute_constraints:

resource:
  aws_cognito_user:
    example:
      user_pool_id: ${aws_cognito_user_pool.example.id}
      username: example
      attributes:
        terraform: true
        foo: bar
        email: no-reply@hashicorp.com
        email_verified: true
```
