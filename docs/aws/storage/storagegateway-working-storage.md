# Storagegateway Working Storage

Manage Storagegateway Working Storage resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_storagegateway_working_storage:
    example:
      disk_id: ${data.aws_storagegateway_local_disk.example.id}
      gateway_arn: ${aws_storagegateway_gateway.example.arn}
```
