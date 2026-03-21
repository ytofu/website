# Resource: aws_cognito_user_group

Provides a Cognito User Group resource.

## Basic Example

```yaml
resource:
  aws_cognito_user_pool:
    main:
      name: identity pool

  aws_iam_role:
    group_role:
      name: user-group-role
      assume_role_policy: ${data.aws_iam_policy_document.group_role.json}

  aws_cognito_user_group:
    main:
      name: user-group
      user_pool_id: ${aws_cognito_user_pool.main.id}
      description: Managed by Terraform
      precedence: 42
      role_arn: ${aws_iam_role.group_role.arn}

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
            - authenticated```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the user group.
* `user_pool_id` - (Required) The user pool ID.
* `description` - (Optional) The description of the user group.
* `precedence` - (Optional) The precedence of the user group.
* `role_arn` - (Optional) The ARN of the IAM role to be associated with the user group.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_cognito_user_group.group us-east-1_vG78M4goG/user-group
```
