# Grafana Workspace Service Account Token

Manage Grafana Workspace Service Account Token resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_grafana_workspace_service_account:
    example:
      name: example-admin
      grafana_role: ADMIN
      workspace_id: ${aws_grafana_workspace.example.id}

resource:
  aws_grafana_workspace_service_account_token:
    example:
      name: example-key
      service_account_id: ${aws_grafana_workspace_service_account.example.service_account_id}
      seconds_to_live: 3600
      workspace_id: ${aws_grafana_workspace.example.id}
```
