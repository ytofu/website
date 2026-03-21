# Resource: aws_sesv2_dedicated_ip_assignment

ytofu resource for managing an AWS SESv2 (Simple Email V2) Dedicated IP Assignment.

## Basic Example

```yaml
resource:
  aws_sesv2_dedicated_ip_assignment:
    example:
      ip: 0.0.0.0
      destination_pool_name: my-pool
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `ip` - (Required) Dedicated IP address.
* `destination_pool_name` - (Required) Dedicated IP address.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - A comma-separated string made up of `ip` and `destination_pool_name`.

## Import

```bash
ytofu import aws_sesv2_dedicated_ip_assignment.example "0.0.0.0,my-pool"
```
