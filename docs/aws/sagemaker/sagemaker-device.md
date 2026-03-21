# Sagemaker Device

Manage Sagemaker Device resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_device:
    example:
      device_fleet_name: ${aws_sagemaker_device_fleet.example.device_fleet_name}
      device:
        device_name: example
```
