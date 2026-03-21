# Guardduty Detector Feature

Manage Guardduty Detector Feature resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_guardduty_detector:
    example:
      enable: true

resource:
  aws_guardduty_detector_feature:
    s3_protection:
      detector_id: ${aws_guardduty_detector.example.id}
      name: S3_DATA_EVENTS
      status: ENABLED
```
