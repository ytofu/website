# Guardduty Member Detector Feature

Manage Guardduty Member Detector Feature resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_guardduty_detector:
    example:
      enable: true

resource:
  aws_guardduty_member_detector_feature:
    runtime_monitoring:
      detector_id: ${aws_guardduty_detector.example.id}
      account_id: 123456789012
      name: S3_DATA_EVENTS
      status: ENABLED
```
