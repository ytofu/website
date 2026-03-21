# Backup Logically Air Gapped Vault

Manage Backup Logically Air Gapped Vault resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_backup_logically_air_gapped_vault:
    example:
      name: lag-example-vault
      max_retention_days: 7
      min_retention_days: 7
```
