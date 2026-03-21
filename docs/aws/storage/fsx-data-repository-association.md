# FSX Data Repository Association

Manage FSX Data Repository Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: my-bucket

resource:
  aws_s3_bucket_acl:
    example:
      bucket: ${aws_s3_bucket.example.id}
      acl: private

resource:
  aws_fsx_lustre_file_system:
    example:
      storage_capacity: 1200
      subnet_ids: 
        - ${aws_subnet.example.id}
      deployment_type: PERSISTENT_2
      per_unit_storage_throughput: 125

resource:
  aws_fsx_data_repository_association:
    example:
      file_system_id: ${aws_fsx_lustre_file_system.example.id}
      data_repository_path: "s3://${aws_s3_bucket.example.id}"
      file_system_path: /my-bucket
      s3:
        auto_export_policy:
          events: 
            - NEW
            - CHANGED
            - DELETED
        auto_import_policy:
          events: 
            - NEW
            - CHANGED
            - DELETED
```
