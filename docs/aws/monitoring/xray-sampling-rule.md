# Xray Sampling Rule

Manage Xray Sampling Rule resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_xray_sampling_rule:
    example:
      rule_name: example
      priority: 9999
      version: 1
      reservoir_size: 1
      fixed_rate: 0.05
      url_path: "*"
      host: "*"
      http_method: "*"
      service_type: "*"
      service_name: "*"
      resource_arn: "*"
      attributes:
        Hello: Tris
```
