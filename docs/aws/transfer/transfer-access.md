# Transfer Access

Manage Transfer Access resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_transfer_access:
    example:
      external_id: S-1-1-12-1234567890-123456789-1234567890-1234
      server_id: ${aws_transfer_server.example.id}
      role: ${aws_iam_role.example.arn}
      home_directory: "/${aws_s3_bucket.example.id}/"
```

## Basic EFS

```yaml
resource:
  aws_transfer_access:
    test:
      external_id: S-1-1-12-1234567890-123456789-1234567890-1234
      server_id: ${aws_transfer_server.test.id}
      role: ${aws_iam_role.test.arn}
      home_directory: "/${aws_efs_file_system.test.id}/"
      posix_profile:
        gid: 1000
        uid: 1000
```
