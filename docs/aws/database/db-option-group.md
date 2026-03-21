# Resource: aws_db_option_group

Provides an RDS DB option group resource. Documentation of the available options for various RDS engines can be found at:

## Basic Example

```yaml
resource:
  aws_db_option_group:
    example:
      name: option-group-test-terraform
      option_group_description: Terraform Option Group
      engine_name: sqlserver-ee
      major_engine_version: 11.00
      option:
        option_name: Timezone
        option_settings:
          name: TIME_ZONE
          value: UTC
      option:
        option_name: SQLSERVER_BACKUP_RESTORE
        option_settings:
          name: IAM_ROLE_ARN
          value: ${aws_iam_role.example.arn}
      option:
        option_name: TDE
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Optional, Forces new resource) Name of the option group. If omitted, ytofu will assign a random, unique name. Must be lowercase, to match as it is stored in AWS.
* `name_prefix` - (Optional, Forces new resource) Creates a unique name beginning with the specified prefix. Conflicts with `name`. Must be lowercase, to match as it is stored in AWS.
* `option_group_description` - (Optional) Description of the option group. Defaults to "Managed by ytofu".
* `engine_name` - (Required) Specifies the name of the engine that this option group should be associated with.
* `major_engine_version` - (Required) Specifies the major version of the engine that this option group should be associated with.
* `option` - (Optional) The options to apply. See [`option` Block](#option-block) below for more details.
* `skip_destroy` - (Optional) Set to true if you do not wish the option group to be deleted at destroy time, and instead just remove the option group from the ytofu state.
* `tags` - (Optional) Map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### `option` Block

The `option` blocks support the following arguments:

* `option_name` - (Required) Name of the option (e.g., MEMCACHED).
* `option_settings` - (Optional) The option settings to apply. See [`option_settings` Block](#option_settings-block) below for more details.
* `port` - (Optional) Port number when connecting to the option (e.g., 11211). Leaving out or removing `port` from your configuration does not remove or clear a port from the option in AWS. AWS may assign a default port. Not including `port` in your configuration means that the AWS provider will ignore a previously set value, a value set by AWS, and any port changes.
* `version` - (Optional) Version of the option (e.g., 13.1.0.0). Leaving out or removing `version` from your configuration does not remove or clear a version from the option in AWS. AWS may assign a default version. Not including `version` in your configuration means that the AWS provider will ignore a previously set value, a value set by AWS, and any version changes.
* `db_security_group_memberships` - (Optional) List of DB Security Groups for which the option is enabled.
* `vpc_security_group_memberships` - (Optional) List of VPC Security Groups for which the option is enabled.

#### `option_settings` Block

The `option_settings` blocks support the following arguments:

* `name` - (Required) Name of the setting.
* `value` - (Required) Value of the setting.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - DB option group name.
* `arn` - ARN of the DB option group.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

- `delete` - (Default `15m`)

## Import

```bash
ytofu import aws_db_option_group.example mysql-option-group
```
