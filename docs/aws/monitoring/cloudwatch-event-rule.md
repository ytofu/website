# CloudWatch Event Rule (EventBridge)

Create event rules for event-driven automation using ytofu YAML.

## Scheduled Rule

```yaml
resource:
  aws_cloudwatch_event_rule:
    every_hour:
      name: every-hour
      description: Fires every hour
      schedule_expression: rate(1 hour)
```

## EC2 State Change Event

```yaml
resource:
  aws_cloudwatch_event_rule:
    ec2_state:
      name: capture-ec2-state-changes
      description: Capture EC2 instance state changes
      event_pattern: |
        {
          "source": ["aws.ec2"],
          "detail-type": ["EC2 Instance State-change Notification"],
          "detail": {
            "state": ["stopped", "terminated"]
          }
        }
```

## Console Sign-In Event

```yaml
resource:
  aws_cloudwatch_event_rule:
    console_signin:
      name: capture-console-signin
      event_pattern: |
        {
          "detail-type": ["AWS Console Sign In via CloudTrail"],
          "detail": {
            "eventName": ["ConsoleLogin"]
          }
        }
```
