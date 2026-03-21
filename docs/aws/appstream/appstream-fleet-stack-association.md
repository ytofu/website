# Appstream Fleet Stack Association

Manage Appstream Fleet Stack Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appstream_fleet:
    example:
      name: NAME
      image_name: Amazon-AppStream2-Sample-Image-03-11-2023
      instance_type: stream.standard.small
      compute_capacity:
        desired_instances: 1

resource:
  aws_appstream_stack:
    example:
      name: STACK NAME

resource:
  aws_appstream_fleet_stack_association:
    example:
      fleet_name: ${aws_appstream_fleet.example.name}
      stack_name: ${aws_appstream_stack.example.name}
```
