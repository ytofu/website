# Resource: aws_lightsail_lb_attachment

Manages a Lightsail Load Balancer Attachment. Use this resource to attach Lightsail instances to a load balancer for distributing traffic across multiple instances.

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

## Argument Reference

The following arguments are required:

* `instance_name` - (Required) Name of the instance to attach to the load balancer.
* `lb_name` - (Required) Name of the Lightsail load balancer.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Combination of attributes to create a unique ID: `lb_name`,`instance_name`.

## Import

```bash
ytofu import aws_lightsail_lb_attachment.example example-load-balancer,example-instance
```
