# Ce Anomaly Monitor

Manage Ce Anomaly Monitor resources using ytofu YAML.

## Dimensional Example

```yaml
resource:
  aws_ce_anomaly_monitor:
    service_monitor:
      name: AWSServiceMonitor
      monitor_type: DIMENSIONAL
      monitor_dimension: SERVICE
```

## Custom Example

```yaml
resource:
  aws_ce_anomaly_monitor:
    test:
      name: AWSCustomAnomalyMonitor
      monitor_type: CUSTOM
      monitor_specification: '{ "And": null "CostCategories": null "Dimensions": null "Not": null "Or": null "Tags": { "Key": "CostCenter" "MatchOptions": null "Values": [ "10000" ] } }'
```
