# Servicequotas Template

Manage Servicequotas Template resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_servicequotas_template:
    example:
      aws_region: us-east-1
      quota_code: "L-2ACBD22F" # function and layer storage (default: 75 GB)
      service_code: lambda
      value: 80
```
