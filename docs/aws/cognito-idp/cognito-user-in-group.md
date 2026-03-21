# Resource: aws_cognito_user_in_group

Adds the specified user to the specified group.

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `user_pool_id` - (Required) The user pool ID of the user and group.
* `group_name` - (Required) The name of the group to which the user is to be added.
* `username` - (Required) The username of the user to be added to the group.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_cognito_user_in_group.example us-east-1_vG78M4goG,example-group,example-user
```
