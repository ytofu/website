# Backup Restore Testing Selection

Manage Backup Restore Testing Selection resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_backup_restore_testing_selection:
    example:
      name: ec2_selection
      restore_testing_plan_name: ${aws_backup_restore_testing_plan.example.name}
      protected_resource_type: EC2
      iam_role_arn: ${aws_iam_role.example.arn}
      protected_resource_arns: 
        - "*"
```

## Advanced Usage

```yaml
resource:
  aws_backup_restore_testing_selection:
    example:
      name: ec2_selection
      restore_testing_plan_name: ${aws_backup_restore_testing_plan.example.name}
      protected_resource_type: EC2
      iam_role_arn: ${aws_iam_role.example.arn}
      protected_resource_conditions:
        string_equals:
          key: "aws:ResourceTag/backup"
          value: true
```
