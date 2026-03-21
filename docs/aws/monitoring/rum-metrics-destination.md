# Rum Metrics Destination

Manage Rum Metrics Destination resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_rum_metrics_destination:
    example:
      app_monitor_name: ${aws_rum_app_monitor.example.name}
      destination: CloudWatch
```
