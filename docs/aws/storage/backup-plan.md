# Backup Plan

Manage Backup Plan resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_backup_plan:
    example:
      name: tf_example_backup_plan
      rule:
        rule_name: tf_example_backup_rule
        target_vault_name: ${aws_backup_vault.test.name}
        schedule: "cron(0 12 * * ? *)"
        lifecycle:
          delete_after: 14
      advanced_backup_setting:
        backup_options:
          WindowsVSS: enabled
        resource_type: EC2
```
