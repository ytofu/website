# Resource: aws_lightsail_static_ip

Manages a static IP address.

## Basic Example

```yaml
resource:
  aws_lightsail_static_ip:
    example:
      name: example
```

## Argument Reference

The following arguments are required:

* `name` - (Required) Name for the allocated static IP.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Lightsail static IP.
* `ip_address` - Allocated static IP address.
* `support_code` - Support code for the static IP. Include this code in your email to support when you have questions about a static IP in Lightsail. This code enables our support team to look up your Lightsail information more easily.

## Import

```bash
ytofu import aws_lightsail_static_ip.example example
```
