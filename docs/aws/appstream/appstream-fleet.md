# Appstream Fleet

Manage Appstream Fleet resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appstream_fleet:
    test_fleet:
      name: test-fleet
      compute_capacity:
        desired_instances: 1
      description: test fleet
      idle_disconnect_timeout_in_seconds: 60
      display_name: test-fleet
      enable_default_internet_access: false
      fleet_type: ON_DEMAND
      image_name: Amazon-AppStream2-Sample-Image-03-11-2023
      instance_type: stream.standard.large
      max_user_duration_in_seconds: 600
      vpc_config:
        subnet_ids: 
          - subnet-06e9b13400c225127
      tags:
        TagName: tag-value
```
