# Lightsail Disk

Manage Lightsail Disk resources using ytofu YAML.

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
```
