# Storagegateway Upload Buffer

Manage Storagegateway Upload Buffer resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_storagegateway_local_disk:
    test:
      disk_node: ${aws_volume_attachment.test.device_name}
      gateway_arn: ${aws_storagegateway_gateway.test.arn}

resource:
  aws_storagegateway_upload_buffer:
    test:
      disk_path: ${data.aws_storagegateway_local_disk.test.disk_path}
      gateway_arn: ${aws_storagegateway_gateway.test.arn}
```

## Stored Gateway Type

```yaml
data:
  aws_storagegateway_local_disk:
    test:
      disk_node: ${aws_volume_attachment.test.device_name}
      gateway_arn: ${aws_storagegateway_gateway.test.arn}

resource:
  aws_storagegateway_upload_buffer:
    example:
      disk_id: ${data.aws_storagegateway_local_disk.example.id}
      gateway_arn: ${aws_storagegateway_gateway.example.arn}
```
