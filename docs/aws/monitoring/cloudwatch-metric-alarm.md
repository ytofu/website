# Cloudwatch Metric Alarm

Manage Cloudwatch Metric Alarm resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudwatch_metric_alarm:
    foobar:
      alarm_name: terraform-test-foobar5
      comparison_operator: GreaterThanOrEqualToThreshold
      evaluation_periods: 2
      metric_name: CPUUtilization
      namespace: AWS/EC2
      period: 120
      statistic: Average
      threshold: 80
      alarm_description: This metric monitors ec2 cpu utilization
      insufficient_data_actions: []
```

## With Scaling Policies

```yaml
resource:
  aws_autoscaling_policy:
    bat:
      name: foobar3-terraform-test
      scaling_adjustment: 4
      adjustment_type: ChangeInCapacity
      cooldown: 300
      autoscaling_group_name: ${aws_autoscaling_group.bar.name}

resource:
  aws_cloudwatch_metric_alarm:
    bat:
      alarm_name: terraform-test-foobar5
      comparison_operator: GreaterThanOrEqualToThreshold
      evaluation_periods: 2
      metric_name: CPUUtilization
      namespace: AWS/EC2
      period: 120
      statistic: Average
      threshold: 80
      dimensions:
        AutoScalingGroupName: ${aws_autoscaling_group.bar.name}
      alarm_description: This metric monitors ec2 cpu utilization
      alarm_actions: 
        - ${aws_autoscaling_policy.bat.arn}
```

## With a Metrics Math Expression

```yaml
resource:
  aws_cloudwatch_metric_alarm:
    foobar:
      alarm_name: terraform-test-foobar
      comparison_operator: GreaterThanOrEqualToThreshold
      evaluation_periods: 2
      threshold: 10
      alarm_description: Request error rate has exceeded 10%
      insufficient_data_actions: []
      metric_query:
        id: e1
        expression: "m2/m1*100"
        label: Error Rate
        return_data: true
      metric_query:
        id: m1
        metric:
          metric_name: RequestCount
          namespace: AWS/ApplicationELB
          period: 120
          stat: Sum
          unit: Count
          dimensions:
            LoadBalancer: app/web
      metric_query:
        id: m2
        metric:
          metric_name: HTTPCode_ELB_5XX_Count
          namespace: AWS/ApplicationELB
          period: 120
          stat: Sum
          unit: Count
          dimensions:
            LoadBalancer: app/web
```

## With a Metrics Insights Query

```yaml
resource:
  aws_cloudwatch_metric_alarm:
    example:
      alarm_name: example-alarm
      alarm_description: Triggers if the smallest per-instance maximum load during the evaluation period exceeds the threshold
      comparison_operator: GreaterThanThreshold
      evaluation_periods: 1
      threshold: 0.6
      treat_missing_data: notBreaching
      metric_query:
        id: q1
        expression: |
          SELECT
          MAX(DBLoadRelativeToNumVCPUs)
          FROM SCHEMA("AWS/RDS", DBInstanceIdentifier)
          WHERE DBInstanceIdentifier != 'example-rds-instance'
          GROUP BY DBInstanceIdentifier
          ORDER BY MIN() ASC
          LIMIT 1
        period: 60
        return_data: true
        label: Max DB Load of the Least-Loaded RDS Instance
```

## Monitoring Healthy NLB Hosts with Target Group and NLB

```yaml
resource:
  aws_cloudwatch_metric_alarm:
    nlb_healthyhosts:
      alarm_name: alarmname
      comparison_operator: LessThanThreshold
      evaluation_periods: 1
      metric_name: HealthyHostCount
      namespace: AWS/NetworkELB
      period: 60
      statistic: Average
      threshold: example-logstash_servers_count
      alarm_description: Number of healthy nodes in Target Group
      actions_enabled: true
      alarm_actions: 
        - ${aws_sns_topic.sns.arn}
      ok_actions: 
        - ${aws_sns_topic.sns.arn}
      dimensions:
        TargetGroup: ${aws_lb_target_group.lb-tg.arn_suffix}
        LoadBalancer: ${aws_lb.lb.arn_suffix}
```
