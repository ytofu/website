# Backup Restore Testing Plan

Manage Backup Restore Testing Plan resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_backup_restore_testing_plan:
    example:
      name: example_restore_testing_plan
      recovery_point_selection:
        algorithm: LATEST_WITHIN_WINDOW
        include_vaults: 
          - "*"
        recovery_point_types: 
          - CONTINUOUS
      schedule_expression: "cron(0 12 ? * * *)" # Daily at 12:00
```
