# Resource: aws_athena_capacity_reservation

ytofu resource for managing an AWS Athena Capacity Reservation.

## Basic Example

```yaml
resource:
  aws_athena_capacity_reservation:
    example:
      name: example-reservation
      target_dpus: 24
```

## Argument Reference

The following arguments are required:

* `name` - (Required) Name of the capacity reservation.
* `target_dpus` - (Required) Number of data processing units requested. Must be at least `24` units.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `tags` - (Optional) Map of tags assigned to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `allocated_dpus` - Number of data processing units currently allocated.
* `arn` - ARN of the Capacity Reservation.
* `status` - Status of the capacity reservation.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `create` - (Default `30m`)
* `update` - (Default `30m`)
* `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_athena_capacity_reservation.example example-reservation
```
