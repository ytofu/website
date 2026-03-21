# Resource: aws_ec2_availability_zone_group

Manages an EC2 Availability Zone Group, such as updating its opt-in status.

## Basic Example

```yaml
resource:
  aws_ec2_availability_zone_group:
    example:
      group_name: us-west-2-lax-1
      opt_in_status: opted-in
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `group_name` - (Required) Name of the Availability Zone Group.
* `opt_in_status` - (Required) Indicates whether to enable or disable Availability Zone Group. Valid values: `opted-in` or `not-opted-in`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Name of the Availability Zone Group.

## Import

```bash
ytofu import aws_ec2_availability_zone_group.example us-west-2-lax-1
```
