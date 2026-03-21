# Kinesisanalyticsv2 Application Snapshot

Manage Kinesisanalyticsv2 Application Snapshot resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_kinesisanalyticsv2_application_snapshot:
    example:
      application_name: ${aws_kinesisanalyticsv2_application.example.name}
      snapshot_name: example-snapshot
```
