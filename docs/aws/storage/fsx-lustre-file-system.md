# FSX Lustre File System

Manage FSX Lustre File System resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_fsx_lustre_file_system:
    example:
      import_path: "s3://${aws_s3_bucket.example.bucket}"
      storage_capacity: 1200
      subnet_ids: 
        - ${aws_subnet.example.id}
```
