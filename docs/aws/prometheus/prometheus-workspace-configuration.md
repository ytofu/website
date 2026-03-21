# Resource: aws_prometheus_workspace_configuration

Manages an AWS Managed Service for Prometheus Workspace Configuration.

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

## Argument Reference

The following arguments are required:

* `workspace_id` - (Required) ID of the workspace to configure.

The following arguments are optional:

* `limits_per_label_set` - (Optional) Configuration block for setting limits on metrics with specific label sets. Detailed below.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `retention_period_in_days` - (Optional) Number of days to retain metric data in the workspace.

### `limits_per_label_set`

The `limits_per_label_set` configuration block supports the following arguments:

* `label_set` - (Required) Map of label key-value pairs that identify the metrics to which the limits apply. An empty map represents the default bucket for metrics that don't match any other label set.
* `limits` - (Required) Configuration block for the limits to apply to the specified label set. Detailed below.

#### `limits`

The `limits` configuration block supports the following arguments:

* `max_series` - (Required) Maximum number of active time series that can be ingested for metrics matching the label set.

## Attribute Reference

This resource exports no additional attributes.

## Timeouts

Configuration options:

* `create` - (Default `5m`)
* `update` - (Default `5m`)

## Import

```bash
ytofu import aws_prometheus_workspace_configuration.example ws-12345678-abcd-1234-abcd-123456789012
```
