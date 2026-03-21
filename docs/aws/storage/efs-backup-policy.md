# Resource: aws_efs_backup_policy

Provides an Elastic File System (EFS) Backup Policy resource.
Backup policies turn automatic backups on or off for an existing file system.

## Basic Example

```yaml
resource:
  aws_efs_file_system:
    fs:
      creation_token: my-product

  aws_efs_backup_policy:
    policy:
      file_system_id: ${aws_efs_file_system.fs.id}
      backup_policy:
        status: ENABLED```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `file_system_id` - (Required) The ID of the EFS file system.
* `backup_policy` - (Required) A backup_policy object (documented below).

### Backup Policy Arguments

`backup_policy` supports the following arguments:

* `status` - (Required) A status of the backup policy. Valid values: `ENABLED`, `DISABLED`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID that identifies the file system (e.g., fs-ccfc0d65).

## Import

```bash
ytofu import aws_efs_backup_policy.example fs-6fa144c6
```
