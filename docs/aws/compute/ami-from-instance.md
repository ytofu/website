# Resource: aws_ami_from_instance

The "AMI from instance" resource allows the creation of an Amazon Machine
Image (AMI) modeled after an existing EBS-backed EC2 instance.

## Basic Example

```yaml
resource:
  aws_ami_from_instance:
    example:
      name: terraform-example
      source_instance_id: i-xxxxxxxx
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) Region-unique name for the AMI.
* `source_instance_id` - (Required) ID of the instance to use as the basis of the AMI.
* `snapshot_without_reboot` - (Optional) Boolean that overrides the behavior of stopping
  the instance before snapshotting. This is risky since it may cause a snapshot of an
  inconsistent filesystem state, but can be used to avoid downtime if the user otherwise
  guarantees that no filesystem writes will be underway at the time of snapshot.
* `tags` - (Optional) Map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the AMI.
* `id` - ID of the created AMI.

This resource also exports a full set of attributes corresponding to the arguments of the
`aws_ami` resource, allowing the properties of the created AMI to be used elsewhere in the
configuration.

## Timeouts

Configuration options:

* `create` - (Default `40m`)
* `update` - (Default `40m`)
* `delete` - (Default `90m`)
