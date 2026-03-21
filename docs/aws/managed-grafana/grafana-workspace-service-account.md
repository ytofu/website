# Grafana Workspace Service Account

Manage Grafana Workspace Service Account resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_grafana_workspace_service_account:
    example:
      name: example-admin
      grafana_role: ADMIN
      workspace_id: ${aws_grafana_workspace.example.id}
```
