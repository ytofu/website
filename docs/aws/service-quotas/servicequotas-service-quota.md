# Servicequotas Service Quota

Manage Servicequotas Service Quota resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_servicequotas_service_quota:
    example:
      quota_code: L-F678F1CE
      service_code: vpc
      value: 75
```
