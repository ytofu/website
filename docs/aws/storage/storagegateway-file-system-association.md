# Storagegateway File System Association

Manage Storagegateway File System Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_storagegateway_file_system_association:
    example:
      gateway_arn: ${aws_storagegateway_gateway.example.arn}
      location_arn: ${aws_fsx_windows_file_system.example.arn}
      username: Admin
      password: avoid-plaintext-passwords
      audit_destination_arn: ${aws_s3_bucket.example.arn}
```
