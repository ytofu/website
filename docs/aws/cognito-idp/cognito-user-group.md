# Cognito User Group

Manage Cognito User Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cognito_user_pool:
    main:
      name: identity pool

data:
  aws_iam_policy_document:
    group_role:
      statement:
        effect: Allow
        principals:
          type: Federated
          identifiers: 
            - cognito-identity.amazonaws.com
        actions: 
          - "sts:AssumeRoleWithWebIdentity"
        condition:
          test: StringEquals
          values: 
            - "us-east-1:12345678-dead-beef-cafe-123456790ab"
        condition:
          test: "ForAnyValue:StringLike"
          values: 
            - authenticated

resource:
  aws_iam_role:
    group_role:
      name: user-group-role
      assume_role_policy: ${data.aws_iam_policy_document.group_role.json}

resource:
  aws_cognito_user_group:
    main:
      name: user-group
      user_pool_id: ${aws_cognito_user_pool.main.id}
      description: Managed by Terraform
      precedence: 42
      role_arn: ${aws_iam_role.group_role.arn}
```
