# Prometheus Resource Policy

Manage Prometheus Resource Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_prometheus_workspace:
    example:
      alias: example-workspace

data:
  aws_caller_identity:
    current:

data:
  aws_iam_policy_document:
    example:
      statement:
        effect: Allow
        principals:
          type: AWS
          identifiers: 
            - ${data.aws_caller_identity.current.account_id}
        actions:
          - "aps:RemoteWrite"
          - "aps:QueryMetrics"
          - "aps:GetSeries"
          - "aps:GetLabels"
          - "aps:GetMetricMetadata"
        resources: 
          - ${aws_prometheus_workspace.example.arn}

resource:
  aws_prometheus_resource_policy:
    example:
      workspace_id: ${aws_prometheus_workspace.example.id}
      policy_document: ${data.aws_iam_policy_document.example.json}
```

## Cross-Account Access

```yaml
resource:
  aws_prometheus_workspace:
    example:
      alias: example-workspace

data:
  aws_iam_policy_document:
    cross_account:
      statement:
        effect: Allow
        principals:
          type: AWS
          identifiers: 
            - "arn:aws:iam::123456789012:root"
        actions:
          - "aps:RemoteWrite"
          - "aps:QueryMetrics"
        resources: 
          - ${aws_prometheus_workspace.example.arn}

resource:
  aws_prometheus_resource_policy:
    cross_account:
      workspace_id: ${aws_prometheus_workspace.example.id}
      policy_document: ${data.aws_iam_policy_document.cross_account.json}
```

## Service-Specific Access

```yaml
resource:
  aws_prometheus_workspace:
    example:
      alias: example-workspace

data:
  aws_iam_policy_document:
    service_access:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - grafana.amazonaws.com
        actions:
          - "aps:QueryMetrics"
          - "aps:GetSeries"
          - "aps:GetLabels"
          - "aps:GetMetricMetadata"
        resources: 
          - ${aws_prometheus_workspace.example.arn}

resource:
  aws_prometheus_resource_policy:
    service_access:
      workspace_id: ${aws_prometheus_workspace.example.id}
      policy_document: ${data.aws_iam_policy_document.service_access.json}
```
