# Backup Selection

Manage Backup Selection resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - backup.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    example:
      name: example
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

resource:
  aws_iam_role_policy_attachment:
    example:
      policy_arn: "arn:aws:iam::aws:policy/service-role/AWSBackupServiceRolePolicyForBackup"
      role: ${aws_iam_role.example.name}

resource:
  aws_backup_selection:
    example:
      iam_role_arn: ${aws_iam_role.example.arn}
```

## Selecting Backups By Tag

```yaml
resource:
  aws_backup_selection:
    example:
      iam_role_arn: ${aws_iam_role.example.arn}
      name: tf_example_backup_selection
      plan_id: ${aws_backup_plan.example.id}
      selection_tag:
        type: STRINGEQUALS
        key: foo
        value: bar
```

## Selecting Backups By Conditions

```yaml
resource:
  aws_backup_selection:
    example:
      iam_role_arn: ${aws_iam_role.example.arn}
      name: tf_example_backup_selection
      plan_id: ${aws_backup_plan.example.id}
      resources: 
        - "*"
      condition:
        string_equals:
          key: "aws:ResourceTag/Component"
          value: rds
        string_like:
          key: "aws:ResourceTag/Application"
          value: "app*"
        string_not_equals:
          key: "aws:ResourceTag/Backup"
          value: false
        string_not_like:
          key: "aws:ResourceTag/Environment"
          value: "test*"
```

## Selecting Backups By Resource

```yaml
resource:
  aws_backup_selection:
    example:
      iam_role_arn: ${aws_iam_role.example.arn}
      name: tf_example_backup_selection
      plan_id: ${aws_backup_plan.example.id}
      resources:
        - ${aws_db_instance.example.arn}
        - ${aws_ebs_volume.example.arn}
        - ${aws_efs_file_system.example.arn}
```

## Selecting Backups By Not Resource

```yaml
resource:
  aws_backup_selection:
    example:
      iam_role_arn: ${aws_iam_role.example.arn}
      name: tf_example_backup_selection
      plan_id: ${aws_backup_plan.example.id}
      not_resources:
        - ${aws_db_instance.example.arn}
        - ${aws_ebs_volume.example.arn}
        - ${aws_efs_file_system.example.arn}
```
