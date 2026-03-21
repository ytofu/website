# Resource: aws_redshift_cluster_snapshot

Creates a Redshift cluster snapshot

## Basic Example

```yaml
resource:
  aws_redshift_cluster_snapshot:
    example:
      cluster_snapshot_name: example
      cluster_snapshot_content: 'example-json-policy'
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `cluster_identifier` - (Required, Forces new resource) The cluster identifier for which you want a snapshot.
* `snapshot_identifier` - (Required, Forces new resource) A unique identifier for the snapshot that you are requesting. This identifier must be unique for all snapshots within the Amazon Web Services account.
* `manual_snapshot_retention_period` - (Optional) The number of days that a manual snapshot is retained. If the value is `-1`, the manual snapshot is retained indefinitely. Valid values are -1 and between `1` and `3653`.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) of the snapshot.
* `id` - A unique identifier for the snapshot that you are requesting. This identifiermust be unique for all snapshots within the Amazon Web Services account.
* `kms_key_id` - The Key Management Service (KMS) key ID of the encryption key that was used to encrypt data in the cluster from which the snapshot was taken.
* `owner_account` - For manual snapshots, the Amazon Web Services account used to create or copy the snapshot. For automatic snapshots, the owner of the cluster. The owner can perform all snapshot actions, such as sharing a manual snapshot.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_redshift_cluster_snapshot.test example
```
