# SSO Account Assignment

Assign permission sets to accounts using ytofu YAML.

## Group Assignment

```yaml
resource:
  aws_ssoadmin_account_assignment:
    example:
      instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}
      permission_set_arn: ${aws_ssoadmin_permission_set.example.arn}
      principal_id: ${data.aws_identitystore_group.admins.group_id}
      principal_type: GROUP
      target_id: "123456789012"
      target_type: AWS_ACCOUNT
```

## User Assignment

```yaml
resource:
  aws_ssoadmin_account_assignment:
    example:
      instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}
      permission_set_arn: ${aws_ssoadmin_permission_set.example.arn}
      principal_id: ${data.aws_identitystore_user.example.user_id}
      principal_type: USER
      target_id: "123456789012"
      target_type: AWS_ACCOUNT
```
