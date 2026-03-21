# Resource: aws_lightsail_lb_https_redirection_policy

Manages HTTPS redirection for a Lightsail Load Balancer.

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

resource:
  aws_lightsail_lb_https_redirection_policy:
    example:
      lb_name: ${aws_lightsail_lb.example.name}
      enabled: true
```

## Argument Reference

The following arguments are required:

* `enabled` - (Required) Whether to enable HTTP to HTTPS redirection. `true` to activate HTTP to HTTPS redirection or `false` to deactivate HTTP to HTTPS redirection.
* `lb_name` - (Required) Name of the load balancer to which you want to enable HTTP to HTTPS redirection.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Name used for this load balancer (matches `lb_name`).

## Import

```bash
ytofu import aws_lightsail_lb_https_redirection_policy.example example-load-balancer
```
