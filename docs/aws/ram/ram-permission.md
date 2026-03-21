# Resource: aws_ram_permission

Manages an AWS RAM (Resource Access Manager) Permission.

## Basic Example

```yaml
resource:
  aws_ram_permission:
    example:
      name: custom-backup
      policy_template: |
        {
        "Effect": "Allow",
        "Action": [
        "backup:ListProtectedResourcesByBackupVault",
        "backup:ListRecoveryPointsByBackupVault",
        "backup:DescribeRecoveryPoint",
        "backup:DescribeBackupVault"
        ]
        }
      resource_type: "backup:BackupVault"
      tags:
        Name: custom-backup
```

## Argument Reference

This resource supports the following arguments:

* `name` - (Required) Specifies the name of the customer managed permission. The name must be unique within the AWS Region.
* `policy_template` - (Required) A string in JSON format string that contains the following elements of a resource-based policy: Effect, Action and Condition.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `resource_type` - Specifies the name of the resource type that this customer managed permission applies to. The format is `<service-code>:<resource-type>` and is not case sensitive.
* `tags` - (Optional) A map of tags to assign to the resource share. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the permission.
* `default_version` - Specifies whether the version of the managed permission used by this resource share is the default version for this managed permission.
* `status` - The current status of the permission.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
* `version` - The version of the permission associated with this resource share.

## Timeouts

Configuration options:

* `delete` - (Default `10m`)

## Import

```bash
ytofu import aws_ram_permission.example arn:aws:ram:us-west-1:123456789012:permission/test-permission
```
