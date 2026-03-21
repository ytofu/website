# SSM Service Setting

Manage SSM Service Setting resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ssm_service_setting:
    test_setting:
      setting_id: "arn:aws:ssm:us-east-1:123456789012:servicesetting/ssm/parameter-store/high-throughput-enabled"
      setting_value: true
```
