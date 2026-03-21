# Resource: aws_fsx_backup

Provides a FSx Backup resource.

## Basic Example

```yaml
resource:
  aws_fsx_backup:
    example:
      file_system_id: ${aws_fsx_lustre_file_system.example.id}

  aws_fsx_lustre_file_system:
    example:
      storage_capacity: 1200
      subnet_ids: 
        - ${aws_subnet.example.id}
      deployment_type: PERSISTENT_1
      per_unit_storage_throughput: 50```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `file_system_id` - (Optional) The ID of the file system to back up. Required if backing up Lustre or Windows file systems.
* `tags` - (Optional) A map of tags to assign to the file system. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level. If you have set `copy_tags_to_backups` to true, and you specify one or more tags, no existing file system tags are copied from the file system to the backup.
* `volume_id` - (Optional) The ID of the volume to back up. Required if backing up a ONTAP Volume.

Note - One of `file_system_id` or `volume_id` can be specified. `file_system_id` is used for Lustre and Windows, `volume_id` is used for ONTAP.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name of the backup.
* `id` - Identifier of the backup, e.g., `fs-12345678`
* `kms_key_id` -  The ID of the AWS Key Management Service (AWS KMS) key used to encrypt the backup of the Amazon FSx file system's data at rest.
* `owner_id` - AWS account identifier that created the file system.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
* `type` - The type of the file system backup.

## Timeouts

Configuration options:

* `create` - (Default `10m`)
* `delete` - (Default `10m`)

## Import

```bash
ytofu import aws_fsx_backup.example fs-543ab12b1ca672f33
```
