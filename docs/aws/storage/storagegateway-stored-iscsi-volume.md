# Storagegateway Stored Iscsi Volume

Manage Storagegateway Stored Iscsi Volume resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_storagegateway_stored_iscsi_volume:
    example:
      gateway_arn: ${aws_storagegateway_cache.example.gateway_arn}
      network_interface_id: ${aws_instance.example.private_ip}
      target_name: example
      preserve_existing_data: false
      disk_id: ${data.aws_storagegateway_local_disk.test.id}
```

## Create Stored iSCSI Volume From Snapshot

```yaml
resource:
  aws_storagegateway_stored_iscsi_volume:
    example:
      gateway_arn: ${aws_storagegateway_cache.example.gateway_arn}
      network_interface_id: ${aws_instance.example.private_ip}
      snapshot_id: ${aws_ebs_snapshot.example.id}
      target_name: example
      preserve_existing_data: false
      disk_id: ${data.aws_storagegateway_local_disk.test.id}
```
