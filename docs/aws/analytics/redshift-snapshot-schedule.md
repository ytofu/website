# Resource: aws_redshift_snapshot_schedule

## Example Usage

## Basic Example

```yaml
resource:
  aws_redshift_snapshot_schedule:
    default:
      identifier: tf-redshift-snapshot-schedule
      definitions:
        - rate(12 hours)
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `identifier` - (Optional, Forces new resource) The snapshot schedule identifier. If omitted, ytofu will assign a random, unique identifier.
* `identifier_prefix` - (Optional, Forces new resource) Creates a unique
identifier beginning with the specified prefix. Conflicts with `identifier`.
* `description` - (Optional) The description of the snapshot schedule.
* `definitions` - (Optional) The definition of the snapshot schedule. The definition is made up of schedule expressions, for example `cron(30 12 *)` or `rate(12 hours)`.
* `force_destroy` - (Optional) Whether to destroy all associated clusters with this snapshot schedule on deletion. Must be enabled and applied before attempting deletion.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) of the Redshift Snapshot Schedule.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_redshift_snapshot_schedule.default tf-redshift-snapshot-schedule
```
