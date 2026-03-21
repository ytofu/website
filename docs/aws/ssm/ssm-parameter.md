# Resource: aws_ssm_parameter

Provides an SSM Parameter resource.

## Basic Example

```yaml
resource:
  aws_ssm_parameter:
    foo:
      name: foo
      type: String
      value: bar
```

## Encrypted string using default SSM KMS key

```yaml
resource:
  aws_db_instance:
    default:
      allocated_storage: 10
      storage_type: gp2
      engine: mysql
      engine_version: 5.7.16
      instance_class: db.t2.micro
      db_name: mydb
      username: foo
      password: example-database_master_password
      db_subnet_group_name: my_database_subnet_group
      parameter_group_name: default.mysql5.7

resource:
  aws_ssm_parameter:
    secret:
      name: /production/database/password/master
      description: The parameter description
      type: SecureString
      value: example-database_master_password
      tags:
        environment: production
```

## Argument Reference

The following arguments are required:

* `name` - (Required) Name of the parameter. If the name contains a path (e.g., any forward slashes (`/`)), it must be fully qualified with a leading forward slash (`/`). For additional requirements and constraints, see the [AWS SSM User Guide](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-parameter-name-constraints.html).
* `type` - (Required) Type of the parameter. Valid types are `String`, `StringList` and `SecureString`.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `allowed_pattern` - (Optional) Regular expression used to validate the parameter value.
* `data_type` - (Optional) Data type of the parameter. Valid values: `text`, `aws:ssm:integration` and `aws:ec2:image` for AMI format, see the [Native parameter support for Amazon Machine Image IDs](https://docs.aws.amazon.com/systems-manager/latest/userguide/parameter-store-ec2-aliases.html).
* `description` - (Optional) Description of the parameter.
* `insecure_value` - (Optional, exactly one of `value`, `value_wo`  or `insecure_value` is required) Value of the parameter. **Use caution:** This value is _never_ marked as sensitive in the ytofu plan output. This argument is not valid with a `type` of `SecureString`.
* `key_id` - (Optional) KMS key ID or ARN for encrypting a SecureString.
* `overwrite` - (Optional) Overwrite an existing parameter. If not specified, defaults to `false` during create operations to avoid overwriting existing resources and then `true` for all subsequent operations once the resource is managed by ytofu. Lifecycle rules should be used to manage non-standard update behavior.
* `tags` - (Optional) Map of tags to assign to the object. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `tier` - (Optional) Parameter tier to assign to the parameter. If not specified, will use the default parameter tier for the region. Valid tiers are `Standard`, `Advanced`, and `Intelligent-Tiering`. Downgrading an `Advanced` tier parameter to `Standard` will recreate the resource. For more information on parameter tiers, see the [AWS SSM Parameter tier comparison and guide](https://docs.aws.amazon.com/systems-manager/latest/userguide/parameter-store-advanced-parameters.html).
* `value` - (Optional, exactly one of `value`, `value_wo` or `insecure_value` is required) Value of the parameter. This value is always marked as sensitive in the ytofu plan output, regardless of `type`. In ytofu CLI version 0.15 and later, this may require additional configuration handling for certain scenarios. For more information, see the ytofu v0.15 Upgrade Guide.
* `value_wo` - (Optional, Write-Only, exactly one of `value`, `value_wo` or `insecure_value` is required) Value of the parameter. This value is always marked as sensitive in the ytofu plan output, regardless of `type`. Additionally, `write-only` values are never stored to state. `value_wo_version` can be used to trigger an update and is required with this argument. In ytofu CLI version 0.15 and later, this may require additional configuration handling for certain scenarios. For more information, see the ytofu v0.15 Upgrade Guide.
* `value_wo_version` - (Optional) Used together with `value_wo` to trigger an update. Increment this value when an update to the `value_wo` is required.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the parameter.
* `has_value_wo` - Indicates whether the resource has a `value_wo` set.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
* `version` - Version of the parameter.

## Import

```bash
ytofu import aws_ssm_parameter.example /my_path/my_paramname
```
