# Resource: aws_ebs_volume

Manages a single EBS volume.

## Basic Example

```yaml
resource:
  aws_ebs_volume:
    example:
      availability_zone: us-west-2a
      size: 40
      tags:
        Name: HelloWorld
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `availability_zone` - (Required) Availability zone where the EBS volume will exist.
* `encrypted` - (Optional) If true, the disk will be encrypted.
* `final_snapshot` - (Optional) If true, snapshot will be created before volume deletion. Any tags on the volume will be migrated to the snapshot. By default set to false
* `iops` - (Optional) Amount of IOPS to provision for the disk. Only valid for `type` of `io1`, `io2` or `gp3`.
* `kms_key_id` - (Optional) ARN for the KMS encryption key. When specifying `kms_key_id`, `encrypted` needs to be set to true. Note: ytofu must be running with credentials which have the `GenerateDataKeyWithoutPlaintext` permission on the specified KMS key as required by the [EBS KMS CMK volume provisioning process](https://docs.aws.amazon.com/kms/latest/developerguide/services-ebs.html#ebs-cmk) to prevent a volume from being created and almost immediately deleted.
* `multi_attach_enabled` - (Optional) Specifies whether to enable Amazon EBS Multi-Attach. Multi-Attach is supported on `io1` and `io2` volumes.
* `outpost_arn` - (Optional) Amazon Resource Name (ARN) of the Outpost.
* `size` - (Optional) Size of the drive in GiBs.
* `snapshot_id` (Optional) A snapshot to base the EBS volume off of.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `throughput` - (Optional) Throughput that the volume supports, in MiB/s. Only valid for `type` of `gp3`.
* `type` - (Optional) Type of EBS volume. Can be `standard`, `gp2`, `gp3`, `io1`, `io2`, `sc1` or `st1` (Default: `gp2`).
* `volume_initialization_rate` - (Optional) EBS provisioned rate for volume initialization, in MiB/s, at which to download the snapshot blocks from Amazon S3 to the volume. This argument can only be set if `snapshot_id` is specified.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Volume ARN (e.g., arn:aws:ec2:us-east-1:123456789012:volume/vol-59fcb34e).
* `create_time` - Timestamp when volume creation was initiated.
* `id` - Volume ID (e.g., vol-59fcb34e).
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

- `create` - (Default `5m`)
- `update` - (Default `5m`)
- `delete` - (Default `10m`)

## Import

```bash
ytofu import aws_ebs_volume.id vol-049df61146c4d7901
```
