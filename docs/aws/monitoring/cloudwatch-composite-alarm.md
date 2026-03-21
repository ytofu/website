# Cloudwatch Composite Alarm

Manage Cloudwatch Composite Alarm resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudwatch_composite_alarm:
    example:
      alarm_description: This is a composite alarm!
      alarm_name: example-composite-alarm
      alarm_actions: ${aws_sns_topic.example.arn}
      ok_actions: ${aws_sns_topic.example.arn}
      alarm_rule: |
        ALARM(${aws_cloudwatch_metric_alarm.alpha.alarm_name}) OR
        ALARM(${aws_cloudwatch_metric_alarm.bravo.alarm_name})
      actions_suppressor:
        alarm: suppressor-alarm
        extension_period: 10
        wait_period: 20
```
