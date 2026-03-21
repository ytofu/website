# Resource: aws_redshift_snapshot_copy

ytofu resource for managing an AWS Redshift Snapshot Copy.

## Basic Example

```yaml
resource:
  aws_redshift_snapshot_copy:
    example:
      cluster_identifier: ${aws_redshift_cluster.example.id}
      destination_region: us-east-1
```

## Argument Reference

The following arguments are required:

* `cluster_identifier` - (Required) Identifier of the source cluster.
* `destination_region` - (Required) AWS Region to copy snapshots to.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `manual_snapshot_retention_period` - (Optional) Number of days to retain newly copied snapshots in the destination AWS Region after they are copied from the source AWS Region. If the value is `-1`, the manual snapshot is retained indefinitely.
* `retention_period` - (Optional) Number of days to retain automated snapshots in the destination region after they are copied from the source region.
* `snapshot_copy_grant_name` - (Optional) Name of the snapshot copy grant to use when snapshots of an AWS KMS-encrypted cluster are copied to the destination region.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Identifier of the source cluster.

## Import

```bash
ytofu import aws_redshift_snapshot_copy.example cluster-id-12345678
```
