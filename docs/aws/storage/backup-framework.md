# Backup Framework

Manage Backup Framework resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_backup_framework:
    Example:
      name: exampleFramework
      description: this is an example framework
      control:
        name: BACKUP_RECOVERY_POINT_MINIMUM_RETENTION_CHECK
        input_parameter:
          name: requiredRetentionDays
          value: 35
      control:
        name: BACKUP_PLAN_MIN_FREQUENCY_AND_MIN_RETENTION_CHECK
        input_parameter:
          name: requiredFrequencyUnit
          value: hours
        input_parameter:
          name: requiredRetentionDays
          value: 35
        input_parameter:
          name: requiredFrequencyValue
          value: 1
      control:
        name: BACKUP_RECOVERY_POINT_ENCRYPTED
      control:
        name: BACKUP_RESOURCES_PROTECTED_BY_BACKUP_PLAN
        scope:
          compliance_resource_types:
            - EBS
      control:
        name: BACKUP_RECOVERY_POINT_MANUAL_DELETION_DISABLED
      control:
        name: BACKUP_RESOURCES_PROTECTED_BY_BACKUP_VAULT_LOCK
        input_parameter:
          name: maxRetentionDays
          value: 100
        input_parameter:
          name: minRetentionDays
          value: 1
        scope:
          compliance_resource_types:
            - EBS
      control:
        name: BACKUP_LAST_RECOVERY_POINT_CREATED
        input_parameter:
          name: recoveryPointAgeUnit
          value: days
        input_parameter:
          name: recoveryPointAgeValue
          value: 1
        scope:
          compliance_resource_types:
            - EBS
      tags: 
```
