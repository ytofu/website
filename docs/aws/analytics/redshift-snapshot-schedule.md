# Redshift Snapshot Schedule

Manage Redshift Snapshot Schedule resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_redshift_snapshot_schedule:
    default:
      identifier: tf-redshift-snapshot-schedule
      definitions:
        - rate(12 hours)
```
