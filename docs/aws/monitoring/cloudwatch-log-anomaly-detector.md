# Cloudwatch Log Anomaly Detector

Manage Cloudwatch Log Anomaly Detector resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudwatch_log_group:
    test:
      name: "testing-${count.index}"

resource:
  aws_cloudwatch_log_anomaly_detector:
    test:
      detector_name: testing
      log_group_arn_list: 
        - ${aws_cloudwatch_log_group.test[0].arn}
      anomaly_visibility_time: 7
      evaluation_frequency: TEN_MIN
      enabled: false
```
