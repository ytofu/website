# Resource: aws_efs_replication_configuration

Creates a replica of an existing EFS file system in the same or another region. Creating this resource causes the source EFS file system to be replicated to a new read-only destination EFS file system (unless using the `destination.file_system_id` attribute). Deleting this resource will cause the replication from source to destination to stop and the destination file system will no longer be read only.

## Basic Example

```yaml
resource:
  aws_efs_file_system:
    example:

resource:
  aws_efs_replication_configuration:
    example:
      source_file_system_id: ${aws_efs_file_system.example.id}
      destination:
        region: us-west-2
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `destination` - (Required) A destination configuration block (documented below).
* `source_file_system_id` - (Required) The ID of the file system that is to be replicated.

### Destination Arguments

`destination` supports the following arguments:

* `availability_zone_name` - (Optional) The availability zone in which the replica should be created. If specified, the replica will be created with One Zone storage. If omitted, regional storage will be used.
* `file_system_id` - (Optional) The ID of the destination file system for the replication. If no ID is provided, then EFS creates a new file system with the default settings.
* `kms_key_id` - (Optional) The Key ID, ARN, alias, or alias ARN of the KMS key that should be used to encrypt the replica file system. If omitted, the default KMS key for EFS `/aws/elasticfilesystem` will be used.
* `region` - (Optional) The region in which the replica should be created.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `creation_time` - When the replication configuration was created.
* `destination[0].file_system_id` - The fs ID of the replica.
* `destination[0].status` - The status of the replication.
* `original_source_file_system_arn` - The Amazon Resource Name (ARN) of the original source Amazon EFS file system in the replication configuration.
* `source_file_system_arn` - The Amazon Resource Name (ARN) of the current source file system in the replication configuration.
* `source_file_system_region` - The AWS Region in which the source Amazon EFS file system is located.

## Timeouts

Configuration options:

* `create` - (Default `20m`)
* `delete` - (Default `20m`)

## Import

```bash
ytofu import aws_efs_replication_configuration.example fs-id
```
