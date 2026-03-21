# Resource: aws_db_parameter_group

Provides an RDS DB parameter group resource. Documentation of the available parameters for various RDS engines can be found at:

## Basic Example

```yaml
resource:
  aws_db_parameter_group:
    default:
      name: rds-pg
      family: mysql5.6
      parameter:
        name: character_set_server
        value: utf8
      parameter:
        name: character_set_client
        value: utf8
```

## `create_before_destroy` Lifecycle Configuration

```yaml
resource:
  aws_db_parameter_group:
    example:
      name_prefix: my-pg
      family: postgres13
      parameter:
        name: log_connections
        value: 1
      lifecycle:
        create_before_destroy: true

resource:
  aws_db_instance:
    example:
      parameter_group_name: ${aws_db_parameter_group.example.name}
      apply_immediately: true
```

## Problematic Plan Changes

```yaml
resource:
  aws_db_parameter_group:
    test:
      name: random-test-parameter
      family: mysql5.7
      parameter:
        name: "default_password_lifetime" # same as AWS default
        value: "0"                         # same as AWS default
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Optional, Forces new resource) The name of the DB parameter group. If omitted, ytofu will assign a random, unique name.
* `name_prefix` - (Optional, Forces new resource) Creates a unique name beginning with the specified prefix. Conflicts with `name`.
* `family` - (Required, Forces new resource) The family of the DB parameter group.
* `description` - (Optional, Forces new resource) The description of the DB parameter group. Defaults to "Managed by ytofu".
* `parameter` - (Optional) The DB parameters to apply. See [`parameter` Block](#parameter-block) below for more details. Note that parameters may differ from a family to an other. Full list of all parameters can be discovered via [`aws rds describe-db-parameters`](https://docs.aws.amazon.com/cli/latest/reference/rds/describe-db-parameters.html) after initial creation of the group.
* `skip_destroy` - (Optional) Set to true if you do not wish the parameter group to be deleted at destroy time, and instead just remove the parameter group from the ytofu state.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### `parameter` Block

The `parameter` blocks support the following arguments:

* `name` - (Required) The name of the DB parameter.
* `value` - (Required) The value of the DB parameter.
* `apply_method` - (Optional) "immediate" (default), or "pending-reboot". Some
    engines can't apply some parameters without a reboot, and you will need to
    specify "pending-reboot" here.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The db parameter group name.
* `arn` - The ARN of the db parameter group.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_db_parameter_group.rds_pg rds-pg
```
