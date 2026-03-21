# Lightsail Disk Attachment

Manage Lightsail Disk Attachment resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_availability_zones:
    available:
      state: available
      filter:
        name: opt-in-status
        values: 
          - opt-in-not-required

resource:
  aws_lightsail_disk:
    example:
      name: example-disk
      size_in_gb: 8
      availability_zone: ${data.aws_availability_zones.available.names[0]}

resource:
  aws_lightsail_instance:
    example:
      name: example-instance
      availability_zone: ${data.aws_availability_zones.available.names[0]}
      blueprint_id: amazon_linux_2
      bundle_id: nano_3_0

resource:
  aws_lightsail_disk_attachment:
    example:
      disk_name: ${aws_lightsail_disk.example.name}
      instance_name: ${aws_lightsail_instance.example.name}
      disk_path: /dev/xvdf
```
