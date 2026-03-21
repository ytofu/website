# Resource: aws_ec2_serial_console_access

Provides a resource to manage whether serial console access is enabled for your AWS account in the current AWS region.

## Basic Example

```yaml
resource:
  aws_ec2_serial_console_access:
    example:
      enabled: true
```

## Argument Reference

This resource supports the following arguments:

* `enabled` - (Optional) Whether or not serial console access is enabled. Valid values are `true` or `false`. Defaults to `true`.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_ec2_serial_console_access.example default
```
