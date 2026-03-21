# EBS Snapshot Import

Manage EBS Snapshot Import resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ebs_snapshot_import:
    example:
      disk_container:
        format: VHD
        user_bucket:
          s3_bucket: disk-images
          s3_key: source.vhd
      role_name: disk-image-import
      tags:
        Name: HelloWorld
```
