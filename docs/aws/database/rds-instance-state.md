# Resource: aws_rds_instance_state

ytofu resource for managing an AWS RDS (Relational Database) RDS Instance State.

## Basic Example

```yaml
resource:
  aws_rds_instance_state:
    test:
      identifier: ${aws_db_instance.test.identifier}
      state: available
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `identifier` - (Required) DB Instance Identifier
* `state` - (Required) Configured state of the DB Instance. Valid values are `available` and `stopped`.

## Attribute Reference

This resource exports no additional attributes.

## Timeouts

Configuration options:

* `create` - (Default `30m`)
* `update` - (Default `30m`)

## Import

```bash
ytofu import aws_rds_instance_state.example rds_instance_state-id-12345678
```
