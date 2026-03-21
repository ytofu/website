# Resource: aws_ebs_fast_snapshot_restore

ytofu resource for managing an EBS (Elastic Block Storage) Fast Snapshot Restore.

## Basic Example

```yaml
resource:
  aws_ebs_fast_snapshot_restore:
    example:
      availability_zone: us-west-2a
      snapshot_id: ${aws_ebs_snapshot.example.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `availability_zone` - (Required) Availability zone in which to enable fast snapshot restores.
* `snapshot_id` - (Required) ID of the snapshot.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - A comma-delimited string concatenating `availability_zone` and `snapshot_id`.
* `state` - State of fast snapshot restores. Valid values are `enabling`, `optimizing`, `enabled`, `disabling`, `disabled`.

## Timeouts

Configuration options:

* `create` - (Default `10m`)
* `delete` - (Default `10m`)

## Import

```bash
ytofu import aws_ebs_fast_snapshot_restore.example us-west-2a,snap-abcdef123456
```
