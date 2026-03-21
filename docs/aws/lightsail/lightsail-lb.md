# Lightsail LB

Manage Lightsail LB resources using ytofu YAML.

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
```
