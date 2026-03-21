# Autoscaling Policy

Manage Autoscaling Policy resources using ytofu YAML.

## Basic Example

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
  aws_autoscaling_group:
    bar:
      availability_zones: 
        - us-east-1a
      name: foobar3-terraform-test
      max_size: 5
      min_size: 2
      health_check_grace_period: 300
      health_check_type: ELB
      force_delete: true
      launch_configuration: ${aws_launch_configuration.foo.name}
```

## Create target tracking scaling policy using metric math

```yaml
resource:
  aws_autoscaling_policy:
    example:
      autoscaling_group_name: my-test-asg
      name: foo
      policy_type: TargetTrackingScaling
      target_tracking_configuration:
        target_value: 100
        customized_metric_specification:
          metrics:
            label: Get the queue size (the number of messages waiting to be processed)
            id: m1
            metric_stat:
              metric:
                namespace: AWS/SQS
                metric_name: ApproximateNumberOfMessagesVisible
                dimensions:
                  name: QueueName
                  value: my-queue
              stat: Sum
              period: 10
            return_data: false
          metrics:
            label: Get the group size (the number of InService instances)
            id: m2
            metric_stat:
              metric:
                namespace: AWS/AutoScaling
                metric_name: GroupInServiceInstances
                dimensions:
                  name: AutoScalingGroupName
                  value: my-asg
              stat: Average
              period: 10
            return_data: false
          metrics:
            label: Calculate the backlog per instance
            id: e1
            expression: m1 / m2
            return_data: true
```

## Create predictive scaling policy using customized metrics

```yaml
resource:
  aws_autoscaling_policy:
    example:
      autoscaling_group_name: my-test-asg
      name: foo
      policy_type: PredictiveScaling
      predictive_scaling_configuration:
        metric_specification:
          target_value: 10
          customized_load_metric_specification:
            metric_data_queries:
              id: load_sum
              expression: "SUM(SEARCH('{AWS/EC2,AutoScalingGroupName} MetricName=\"CPUUtilization\" my-test-asg', 'Sum', 3600))"
          customized_capacity_metric_specification:
            metric_data_queries:
              id: capacity_sum
              expression: "SUM(SEARCH('{AWS/AutoScaling,AutoScalingGroupName} MetricName=\"GroupInServiceIntances\" my-test-asg', 'Average', 300))"
          customized_scaling_metric_specification:
            metric_data_queries:
              id: capacity_sum
              expression: "SUM(SEARCH('{AWS/AutoScaling,AutoScalingGroupName} MetricName=\"GroupInServiceIntances\" my-test-asg', 'Average', 300))"
              return_data: false
            metric_data_queries:
              id: load_sum
              expression: "SUM(SEARCH('{AWS/EC2,AutoScalingGroupName} MetricName=\"CPUUtilization\" my-test-asg', 'Sum', 300))"
              return_data: false
            metric_data_queries:
              id: weighted_average
              expression: "load_sum / (capacity_sum * PERIOD(capacity_sum) / 60)"
```

## Create predictive scaling policy using customized scaling and predefined load metric

```yaml
resource:
  aws_autoscaling_policy:
    example:
      autoscaling_group_name: my-test-asg
      name: foo
      policy_type: PredictiveScaling
      predictive_scaling_configuration:
        metric_specification:
          target_value: 10
          predefined_load_metric_specification:
            predefined_metric_type: ASGTotalCPUUtilization
            resource_label: app/my-alb/778d41231b141a0f/targetgroup/my-alb-target-group/943f017f100becff
          customized_scaling_metric_specification:
            metric_data_queries:
              id: scaling
              metric_stat:
                metric:
                  metric_name: CPUUtilization
                  namespace: AWS/EC2
                  dimensions:
                    name: AutoScalingGroupName
                    value: my-test-asg
                stat: Average
```
