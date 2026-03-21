# Resource: aws_sfn_alias

Provides a Step Function State Machine Alias.

## Basic Example

```yaml
resource:
  aws_sfn_alias:
    sfn_alias:
      name: my_sfn_alias
      routing_configuration:
        state_machine_version_arn: ${aws_sfn_state_machine.sfn_test.state_machine_version_arn}
        weight: 100

  aws_sfn_alias:
    my_sfn_alias:
      name: my_sfn_alias
      routing_configuration:
        state_machine_version_arn: "arn:aws:states:us-east-1:12345:stateMachine:demo:3"
        weight: 50
      routing_configuration:
        state_machine_version_arn: "arn:aws:states:us-east-1:12345:stateMachine:demo:2"
        weight: 50```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) Name for the alias you are creating.
* `description` - (Optional) Description of the alias.
* `routing_configuration` - (Required) The StateMachine alias' route configuration settings. Fields documented below

`routing_configuration` supports the following arguments:

* `state_machine_version_arn` - (Required) The Amazon Resource Name (ARN) of the state machine version.
* `weight` - (Required) Percentage of traffic routed to the state machine version.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The Amazon Resource Name (ARN) identifying your state machine alias.
* `creation_date` - The date the state machine alias was created.

## Import

```bash
ytofu import aws_sfn_alias.foo arn:aws:states:us-east-1:123456789098:stateMachine:myStateMachine:foo
```
