# Guardduty Organization Configuration Feature

Manage Guardduty Organization Configuration Feature resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_guardduty_detector:
    example:
      enable: true

resource:
  aws_guardduty_organization_configuration_feature:
    eks_runtime_monitoring:
      detector_id: ${aws_guardduty_detector.example.id}
      name: EKS_RUNTIME_MONITORING
      auto_enable: ALL
      additional_configuration:
        name: EKS_ADDON_MANAGEMENT
        auto_enable: NEW
```
