# Grafana Workspace API Key

Manage Grafana Workspace API Key resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_grafana_workspace_api_key:
    key:
      key_name: test-key
      key_role: VIEWER
      seconds_to_live: 3600
      workspace_id: ${aws_grafana_workspace.test.id}
```
