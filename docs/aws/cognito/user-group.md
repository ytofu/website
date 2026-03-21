# Cognito User Group

Create user groups in Cognito user pools using ytofu YAML.

## Basic Group

```yaml
resource:
  aws_cognito_user_group:
    main:
      name: admin
      user_pool_id: ${aws_cognito_user_pool.main.id}
      description: Admin group
      precedence: 1
      role_arn: ${aws_iam_role.group_role.arn}
```
