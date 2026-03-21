# Resource: aws_appstream_fleet_stack_association

Manages an AppStream Fleet Stack association.

## Basic Example

```yaml
resource:
  aws_appstream_fleet:
    example:
      name: NAME
      image_name: Amazon-AppStream2-Sample-Image-03-11-2023
      instance_type: stream.standard.small
      compute_capacity:
        desired_instances: 1

resource:
  aws_appstream_stack:
    example:
      name: STACK NAME

resource:
  aws_appstream_fleet_stack_association:
    example:
      fleet_name: ${aws_appstream_fleet.example.name}
      stack_name: ${aws_appstream_stack.example.name}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `fleet_name` - (Required) Name of the fleet.
* `stack_name` (Required) Name of the stack.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Unique ID of the appstream stack fleet association, composed of the `fleet_name` and `stack_name` separated by a slash (`/`).

## Import

```bash
ytofu import aws_appstream_fleet_stack_association.example fleetName/stackName
```
