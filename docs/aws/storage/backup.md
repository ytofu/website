# AWS Backup

Configure AWS Backup plans and vaults using ytofu YAML.

## Basic Backup Plan

```yaml
resource:
  aws_backup_vault:
    example:
      name: example-backup-vault

  aws_backup_plan:
    example:
      name: example-backup-plan
      rule:
        - rule_name: daily-backup
          target_vault_name: ${aws_backup_vault.example.name}
          schedule: cron(0 12 * * ? *)
```

## With Lifecycle

```yaml
resource:
  aws_backup_plan:
    example:
      name: example-backup-plan
      rule:
        - rule_name: daily-with-lifecycle
          target_vault_name: ${aws_backup_vault.example.name}
          schedule: cron(0 12 * * ? *)
          lifecycle:
            cold_storage_after: 30
            delete_after: 120
```

## Backup Selection

```yaml
resource:
  aws_backup_selection:
    example:
      iam_role_arn: ${aws_iam_role.backup.arn}
      name: example-backup-selection
      plan_id: ${aws_backup_plan.example.id}
      selection_tag:
        - type: STRINGEQUALS
          key: Backup
          value: "true"
```

## With Copy Action (Cross-Region)

```yaml
resource:
  aws_backup_plan:
    example:
      name: cross-region-backup
      rule:
        - rule_name: daily-cross-region
          target_vault_name: ${aws_backup_vault.example.name}
          schedule: cron(0 12 * * ? *)
          copy_action:
            - destination_vault_arn: ${aws_backup_vault.secondary.arn}
              lifecycle:
                delete_after: 60
```
