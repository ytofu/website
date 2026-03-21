# Route53recoveryreadiness Resource Set

Manage Route53recoveryreadiness Resource Set resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_route53recoveryreadiness_resource_set:
    example:
      resource_set_name: my-cw-alarm-set
      resource_set_type: "AWS::CloudWatch::Alarm"
      resources:
        resource_arn: ${aws_cloudwatch_metric_alarm.example.arn}
```
