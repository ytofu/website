# FSX S3 Access Point Attachment

Manage FSX S3 Access Point Attachment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_fsx_s3_access_point_attachment:
    example:
      name: example-attachment
      type: OPENZFS
      openzfs_configuration:
        volume_id: ${aws_fsx_openzfs_volume.example.id}
        file_system_identity:
          type: POSIX
          posix_user:
            uid: 1001
            gid: 1001
```
