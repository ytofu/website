# Resource: aws_backup_vault_policy

Provides an AWS Backup vault policy resource.

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `backup_vault_name` - (Required) Name of the backup vault to add policy for.
* `policy` - (Required) The backup vault access policy document in JSON format.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The name of the vault.
* `backup_vault_arn` - The ARN of the vault.

## Import

```bash
ytofu import aws_backup_vault_policy.test TestVault
```
