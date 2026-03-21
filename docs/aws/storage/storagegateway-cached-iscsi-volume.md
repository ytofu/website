# Resource: aws_storagegateway_cached_iscsi_volume

Manages an AWS Storage Gateway cached iSCSI volume.

## Create Empty Cached iSCSI Volume

```yaml
resource:
  aws_storagegateway_cached_iscsi_volume:
    example:
      gateway_arn: ${aws_storagegateway_cache.example.gateway_arn}
      network_interface_id: ${aws_instance.example.private_ip}
      target_name: example
      volume_size_in_bytes: 5368709120
```

## Create Cached iSCSI Volume From Snapshot

```yaml
resource:
  aws_storagegateway_cached_iscsi_volume:
    example:
      gateway_arn: ${aws_storagegateway_cache.example.gateway_arn}
      network_interface_id: ${aws_instance.example.private_ip}
      snapshot_id: ${aws_ebs_snapshot.example.id}
      target_name: example
      volume_size_in_bytes: ${aws_ebs_snapshot.example.volume_size * 1024 * 1024 * 1024}
```

## Create Cached iSCSI Volume From Source Volume

```yaml
resource:
  aws_storagegateway_cached_iscsi_volume:
    example:
      gateway_arn: ${aws_storagegateway_cache.example.gateway_arn}
      network_interface_id: ${aws_instance.example.private_ip}
      source_volume_arn: ${aws_storagegateway_cached_iscsi_volume.existing.arn}
      target_name: example
      volume_size_in_bytes: ${aws_storagegateway_cached_iscsi_volume.existing.volume_size_in_bytes}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `gateway_arn` - (Required) The Amazon Resource Name (ARN) of the gateway.
* `network_interface_id` - (Required) The network interface of the gateway on which to expose the iSCSI target. Only IPv4 addresses are accepted.
* `target_name` - (Required) The name of the iSCSI target used by initiators to connect to the target and as a suffix for the target ARN. The target name must be unique across all volumes of a gateway.
* `volume_size_in_bytes` - (Required) The size of the volume in bytes.
* `snapshot_id` - (Optional) The snapshot ID of the snapshot to restore as the new cached volumeE.g., `snap-1122aabb`.
* `source_volume_arn` - (Optional) The ARN for an existing volume. Specifying this ARN makes the new volume into an exact copy of the specified existing volume's latest recovery point. The `volume_size_in_bytes` value for this new volume must be equal to or larger than the size of the existing volume, in bytes.
* `kms_encrypted` - (Optional) Set to `true` to use Amazon S3 server side encryption with your own AWS KMS key, or `false` to use a key managed by Amazon S3.
* `kms_key` - (Optional) The Amazon Resource Name (ARN) of the AWS KMS key used for Amazon S3 server side encryption. Is required when `kms_encrypted` is set.
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Volume Amazon Resource Name (ARN), e.g., `arn:aws:storagegateway:us-east-1:123456789012:gateway/sgw-12345678/volume/vol-12345678`.
* `chap_enabled` - Whether mutual CHAP is enabled for the iSCSI target.
* `id` - Volume Amazon Resource Name (ARN), e.g., `arn:aws:storagegateway:us-east-1:123456789012:gateway/sgw-12345678/volume/vol-12345678`.
* `lun_number` - Logical disk number.
* `network_interface_port` - The port used to communicate with iSCSI targets.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
* `target_arn` - Target Amazon Resource Name (ARN), e.g., `arn:aws:storagegateway:us-east-1:123456789012:gateway/sgw-12345678/target/iqn.1997-05.com.amazon:TargetName`.
* `volume_arn` - Volume Amazon Resource Name (ARN), e.g., `arn:aws:storagegateway:us-east-1:123456789012:gateway/sgw-12345678/volume/vol-12345678`.
* `volume_id` - Volume ID, e.g., `vol-12345678`.

## Import

```bash
ytofu import aws_storagegateway_cached_iscsi_volume.example arn:aws:storagegateway:us-east-1:123456789012:gateway/sgw-12345678/volume/vol-12345678
```
