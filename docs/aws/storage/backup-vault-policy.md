# Backup Vault Policy

Manage Backup Vault Policy resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_backup_vault:
    example:
      name: example

data:
  aws_iam_policy_document:
    example:
      statement:
        effect: Allow
        principals:
          type: AWS
          identifiers: 
            - ${data.aws_caller_identity.current.account_id}
        actions:
          - "backup:DescribeBackupVault"
          - "backup:DeleteBackupVault"
          - "backup:PutBackupVaultAccessPolicy"
          - "backup:DeleteBackupVaultAccessPolicy"
          - "backup:GetBackupVaultAccessPolicy"
          - "backup:StartBackupJob"
          - "backup:GetBackupVaultNotifications"
          - "backup:PutBackupVaultNotifications"
        resources: 
          - ${aws_backup_vault.example.arn}

resource:
  aws_backup_vault_policy:
    example:
      backup_vault_name: ${aws_backup_vault.example.name}
      policy: ${data.aws_iam_policy_document.example.json}
```
