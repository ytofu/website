# Route53recoverycontrolconfig Safety Rule

Manage Route53recoverycontrolconfig Safety Rule resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_route53recoverycontrolconfig_safety_rule:
    example:
      asserted_controls: 
        - ${aws_route53recoverycontrolconfig_routing_control.example.arn}
      control_panel_arn: "arn:aws:route53-recovery-control::313517334327:controlpanel/abd5fbfc052d4844a082dbf400f61da8"
      name: daisyguttridge
      wait_period_ms: 5000
      rule_config:
        inverted: false
        threshold: 1
        type: ATLEAST
```
