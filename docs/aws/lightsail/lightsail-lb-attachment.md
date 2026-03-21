# Lightsail LB Attachment

Manage Lightsail LB Attachment resources using ytofu YAML.

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
  aws_lightsail_lb:
    example:
      name: example-load-balancer
      health_check_path: /
      instance_port: 80
      tags:
        foo: bar

resource:
  aws_lightsail_instance:
    example:
      name: example-instance
      availability_zone: ${data.aws_availability_zones.available.names[0]}
      blueprint_id: amazon_linux_2
      bundle_id: nano_3_0

resource:
  aws_lightsail_lb_attachment:
    example:
      lb_name: ${aws_lightsail_lb.example.name}
      instance_name: ${aws_lightsail_instance.example.name}
```
