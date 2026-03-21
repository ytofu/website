# Prometheus Workspace Configuration

Manage Prometheus Workspace Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_prometheus_workspace:
    example:

resource:
  aws_prometheus_workspace_configuration:
    example:
      workspace_id: ${aws_prometheus_workspace.example.id}
      retention_period_in_days: 60
      limits_per_label_set:
        label_set: 
        limits:
          max_series: 100000
      limits_per_label_set:
        label_set: 
        limits:
          max_series: 400000
```

## Setting up default bucket

```yaml
resource:
  aws_prometheus_workspace:
    example:

resource:
  aws_prometheus_workspace_configuration:
    example:
      workspace_id: ${aws_prometheus_workspace.example.id}
      limits_per_label_set:
        label_set: {}
        limits:
          max_series: 50000
```
