# Resource: aws_lightsail_static_ip_attachment

Manages a static IP address attachment - relationship between a Lightsail static IP and Lightsail instance.

## Basic Example

```yaml
resource:
  aws_lightsail_static_ip:
    example:
      name: example

resource:
  aws_lightsail_instance:
    example:
      name: example
      availability_zone: us-east-1a
      blueprint_id: ubuntu_20_04
      bundle_id: nano_2_0

resource:
  aws_lightsail_static_ip_attachment:
    example:
      static_ip_name: ${aws_lightsail_static_ip.example.name}
      instance_name: ${aws_lightsail_instance.example.name}
```

## Argument Reference

The following arguments are required:

* `instance_name` - (Required) Name of the Lightsail instance to attach the IP to.
* `static_ip_name` - (Required) Name of the allocated static IP.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `ip_address` - Allocated static IP address.

## Import

```bash
ytofu import aws_lightsail_static_ip_attachment.example example-static-ip
```
