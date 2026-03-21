# Prometheus Alert Manager Definition

Manage Prometheus Alert Manager Definition resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_prometheus_workspace:
    demo:

resource:
  aws_prometheus_alert_manager_definition:
    demo:
      workspace_id: ${aws_prometheus_workspace.demo.id}
      definition: |
        alertmanager_config: |
        route:
        receiver: 'default'
        receivers:
        - name: 'default'
```
