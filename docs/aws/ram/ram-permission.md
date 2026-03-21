# RAM Permission

Manage RAM Permission resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ram_permission:
    example:
      name: custom-backup
      policy_template: |
        {
        "Effect": "Allow",
        "Action": [
        "backup:ListProtectedResourcesByBackupVault",
        "backup:ListRecoveryPointsByBackupVault",
        "backup:DescribeRecoveryPoint",
        "backup:DescribeBackupVault"
        ]
        }
      resource_type: "backup:BackupVault"
      tags:
        Name: custom-backup
```
