# SFN Alias

Manage SFN Alias resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sfn_alias:
    sfn_alias:
      name: my_sfn_alias
      routing_configuration:
        state_machine_version_arn: ${aws_sfn_state_machine.sfn_test.state_machine_version_arn}
        weight: 100

resource:
  aws_sfn_alias:
    my_sfn_alias:
      name: my_sfn_alias
      routing_configuration:
        state_machine_version_arn: "arn:aws:states:us-east-1:12345:stateMachine:demo:3"
        weight: 50
      routing_configuration:
        state_machine_version_arn: "arn:aws:states:us-east-1:12345:stateMachine:demo:2"
        weight: 50
```
