# Lightsail LB Stickiness Policy

Manage Lightsail LB Stickiness Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lightsail_lb:
    example:
      name: example-load-balancer
      health_check_path: /
      instance_port: 80
      tags:
        foo: bar

resource:
  aws_lightsail_lb_stickiness_policy:
    example:
      lb_name: ${aws_lightsail_lb.example.name}
      cookie_duration: 900
      enabled: true
```
