# Resource: aws_rds_cluster_parameter_group

Provides an RDS DB cluster parameter group resource. Documentation of the available parameters for various Aurora engines can be found at:

## Basic Example

```yaml
resource:
  aws_rds_cluster_parameter_group:
    default:
      name: rds-cluster-pg
      family: aurora5.6
      description: RDS default cluster parameter group
      parameter:
        name: character_set_server
        value: utf8
      parameter:
        name: character_set_client
        value: utf8
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Optional, Forces new resource) The name of the DB cluster parameter group. If omitted, ytofu will assign a random, unique name.
* `name_prefix` - (Optional, Forces new resource) Creates a unique name beginning with the specified prefix. Conflicts with `name`.
* `family` - (Required) The family of the DB cluster parameter group.
* `description` - (Optional) The description of the DB cluster parameter group. Defaults to "Managed by ytofu".
* `parameter` - (Optional) A list of DB parameters to apply. Note that parameters may differ from a family to an other. Full list of all parameters can be discovered via [`aws rds describe-db-cluster-parameters`](https://docs.aws.amazon.com/cli/latest/reference/rds/describe-db-cluster-parameters.html) after initial creation of the group.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

Parameter blocks support the following:

* `name` - (Required) The name of the DB parameter.
* `value` - (Required) The value of the DB parameter.
* `apply_method` - (Optional) "immediate" (default), or "pending-reboot". Some
    engines can't apply some parameters without a reboot, and you will need to
    specify "pending-reboot" here.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The db cluster parameter group name.
* `arn` - The ARN of the db cluster parameter group.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_rds_cluster_parameter_group.cluster_pg production-pg-1
```
