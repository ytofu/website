# SSM Maintenance Window

Manage SSM Maintenance Window resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ssm_maintenance_window:
    production:
      name: maintenance-window-application
      schedule: "cron(0 16 ? * TUE *)"
      duration: 3
      cutoff: 1
```
