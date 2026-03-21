# Lightsail LB Certificate Attachment

Manage Lightsail LB Certificate Attachment resources using ytofu YAML.

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
  aws_lightsail_lb_certificate:
    example:
      name: example-load-balancer-certificate
      lb_name: ${aws_lightsail_lb.example.id}
      domain_name: example.com

resource:
  aws_lightsail_lb_certificate_attachment:
    example:
      lb_name: ${aws_lightsail_lb.example.name}
      certificate_name: ${aws_lightsail_lb_certificate.example.name}
```
