# Resource: aws_prometheus_resource_policy

Manages an Amazon Managed Service for Prometheus (AMP) Resource Policy.

## Basic Example

```yaml
resource:
  aws_prometheus_workspace:
    example:
      alias: example-workspace

  aws_prometheus_resource_policy:
    example:
      workspace_id: ${aws_prometheus_workspace.example.id}
      policy_document: ${data.aws_iam_policy_document.example.json}

data:
  aws_caller_identity:
    current:

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
          - ${aws_prometheus_workspace.example.arn}```

## Cross-Account Access

```yaml
resource:
  aws_prometheus_workspace:
    example:
      alias: example-workspace

  aws_prometheus_resource_policy:
    cross_account:
      workspace_id: ${aws_prometheus_workspace.example.id}
      policy_document: ${data.aws_iam_policy_document.cross_account.json}

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
          - ${aws_prometheus_workspace.example.arn}```

## Service-Specific Access

```yaml
resource:
  aws_prometheus_workspace:
    example:
      alias: example-workspace

  aws_prometheus_resource_policy:
    service_access:
      workspace_id: ${aws_prometheus_workspace.example.id}
      policy_document: ${data.aws_iam_policy_document.service_access.json}

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
          - ${aws_prometheus_workspace.example.arn}```

## Argument Reference

This resource supports the following arguments:

* `workspace_id` - (Required) The ID of the workspace to attach the resource-based policy to.
* `policy_document` - (Required) The JSON policy document to use as the resource-based policy. This policy defines the permissions that other AWS accounts or services have to access your workspace.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `policy_status` - The current status of the resource-based policy. Can be `CREATING`, `ACTIVE`, `UPDATING`, or `DELETING`.
* `revision_id` - The revision ID of the current resource-based policy.

## Timeouts

Configuration options:

- `create` - (Default `5m`)
- `update` - (Default `5m`)
- `delete` - (Default `5m`)

## Import

```bash
ytofu import aws_prometheus_resource_policy.example ws-12345678-90ab-cdef-1234-567890abcdef
```
