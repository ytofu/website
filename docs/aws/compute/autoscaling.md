# Auto Scaling

Automatically scale EC2 capacity with Auto Scaling Groups using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_autoscaling_group:
    web:
      name: web-asg
      vpc_zone_identifier:
        - ${aws_subnet.private_a.id}
        - ${aws_subnet.private_b.id}
      desired_capacity: 2
      min_size: 1
      max_size: 5

      launch_template:
        id: ${aws_launch_template.web.id}
        version: $Latest
```

## Complete Auto Scaling Setup

```yaml
resource:
  aws_autoscaling_group:
    web:
      name: web-asg
      vpc_zone_identifier:
        - ${aws_subnet.private_a.id}
        - ${aws_subnet.private_b.id}
      desired_capacity: 2
      min_size: 1
      max_size: 10

      launch_template:
        id: ${aws_launch_template.web.id}
        version: $Latest

      target_group_arns:
        - ${aws_lb_target_group.web.arn}

      health_check_type: ELB
      health_check_grace_period: 300

      instance_refresh:
        strategy: Rolling
        preferences:
          min_healthy_percentage: 75
          instance_warmup: 300

      tag:
        - key: Name
          value: web-server
          propagate_at_launch: true

        - key: Environment
          value: production
          propagate_at_launch: true
```

## Arguments Reference

| Argument | Type | Required | Description |
|----------|------|----------|-------------|
| name | string | No | ASG name |
| vpc_zone_identifier | list | No | Subnet IDs |
| desired_capacity | number | No | Desired instance count |
| min_size | number | Yes | Minimum instances |
| max_size | number | Yes | Maximum instances |
| launch_template | object | No | Launch template config |
| target_group_arns | list | No | Target group ARNs |
| health_check_type | string | No | EC2 or ELB |
| health_check_grace_period | number | No | Seconds before health check |
| instance_refresh | object | No | Rolling update config |
| tag | list | No | Instance tags |

## Common Patterns

### With Load Balancer

```yaml
resource:
  aws_autoscaling_group:
    web:
      name: web-asg
      vpc_zone_identifier:
        - ${aws_subnet.private_a.id}
        - ${aws_subnet.private_b.id}
      desired_capacity: 2
      min_size: 1
      max_size: 10

      launch_template:
        id: ${aws_launch_template.web.id}
        version: $Latest

      target_group_arns:
        - ${aws_lb_target_group.web.arn}

      health_check_type: ELB
      health_check_grace_period: 300

      # Wait for instances to be healthy
      wait_for_capacity_timeout: "10m"
```

### Mixed Instances (Spot + On-Demand)

```yaml
resource:
  aws_autoscaling_group:
    mixed:
      name: mixed-asg
      vpc_zone_identifier:
        - ${aws_subnet.private_a.id}
        - ${aws_subnet.private_b.id}
      desired_capacity: 6
      min_size: 2
      max_size: 20

      mixed_instances_policy:
        instances_distribution:
          on_demand_base_capacity: 2
          on_demand_percentage_above_base_capacity: 25
          spot_allocation_strategy: capacity-optimized
          spot_max_price: ""  # Use on-demand price

        launch_template:
          launch_template_specification:
            launch_template_id: ${aws_launch_template.app.id}
            version: $Latest

          override:
            - instance_type: t3.medium
              weighted_capacity: "1"
            - instance_type: t3.large
              weighted_capacity: "2"
            - instance_type: t3a.medium
              weighted_capacity: "1"
            - instance_type: t3a.large
              weighted_capacity: "2"
```

### Target Tracking Scaling

```yaml
resource:
  aws_autoscaling_group:
    app:
      name: app-asg
      vpc_zone_identifier:
        - ${aws_subnet.private_a.id}
        - ${aws_subnet.private_b.id}
      desired_capacity: 2
      min_size: 1
      max_size: 10

      launch_template:
        id: ${aws_launch_template.app.id}
        version: $Latest

  # CPU-based scaling
  aws_autoscaling_policy:
    cpu:
      name: cpu-scaling
      autoscaling_group_name: ${aws_autoscaling_group.app.name}
      policy_type: TargetTrackingScaling

      target_tracking_configuration:
        predefined_metric_specification:
          predefined_metric_type: ASGAverageCPUUtilization
        target_value: 70
        disable_scale_in: false

  # Request count scaling (with ALB)
  aws_autoscaling_policy:
    requests:
      name: request-scaling
      autoscaling_group_name: ${aws_autoscaling_group.app.name}
      policy_type: TargetTrackingScaling

      target_tracking_configuration:
        predefined_metric_specification:
          predefined_metric_type: ALBRequestCountPerTarget
          resource_label: ${join("/", [
            aws_lb.main.arn_suffix,
            aws_lb_target_group.app.arn_suffix
          ])}
        target_value: 1000
```

### Step Scaling

```yaml
resource:
  aws_autoscaling_policy:
    scale_out:
      name: scale-out
      autoscaling_group_name: ${aws_autoscaling_group.app.name}
      policy_type: StepScaling
      adjustment_type: ChangeInCapacity

      step_adjustment:
        - scaling_adjustment: 1
          metric_interval_lower_bound: 0
          metric_interval_upper_bound: 20

        - scaling_adjustment: 2
          metric_interval_lower_bound: 20
          metric_interval_upper_bound: 40

        - scaling_adjustment: 3
          metric_interval_lower_bound: 40

  aws_cloudwatch_metric_alarm:
    high_cpu:
      alarm_name: high-cpu
      comparison_operator: GreaterThanThreshold
      evaluation_periods: 2
      metric_name: CPUUtilization
      namespace: AWS/EC2
      period: 60
      statistic: Average
      threshold: 70

      dimensions:
        AutoScalingGroupName: ${aws_autoscaling_group.app.name}

      alarm_actions:
        - ${aws_autoscaling_policy.scale_out.arn}
```

### Scheduled Scaling

```yaml
resource:
  # Scale up for business hours
  aws_autoscaling_schedule:
    scale_up:
      scheduled_action_name: scale-up
      autoscaling_group_name: ${aws_autoscaling_group.app.name}
      min_size: 4
      max_size: 20
      desired_capacity: 8
      recurrence: "0 8 * * MON-FRI"  # 8 AM weekdays
      time_zone: America/New_York

  # Scale down after hours
  aws_autoscaling_schedule:
    scale_down:
      scheduled_action_name: scale-down
      autoscaling_group_name: ${aws_autoscaling_group.app.name}
      min_size: 1
      max_size: 5
      desired_capacity: 2
      recurrence: "0 20 * * MON-FRI"  # 8 PM weekdays
      time_zone: America/New_York
```

### Predictive Scaling

```yaml
resource:
  aws_autoscaling_policy:
    predictive:
      name: predictive-scaling
      autoscaling_group_name: ${aws_autoscaling_group.app.name}
      policy_type: PredictiveScaling

      predictive_scaling_configuration:
        mode: ForecastAndScale
        scheduling_buffer_time: 300

        metric_specification:
          target_value: 70

          predefined_scaling_metric_specification:
            predefined_metric_type: ASGAverageCPUUtilization
            resource_label: ""

          predefined_load_metric_specification:
            predefined_metric_type: ASGTotalCPUUtilization
            resource_label: ""
```

### Instance Refresh (Rolling Updates)

```yaml
resource:
  aws_autoscaling_group:
    app:
      name: app-asg
      vpc_zone_identifier:
        - ${aws_subnet.private_a.id}
        - ${aws_subnet.private_b.id}
      desired_capacity: 4
      min_size: 2
      max_size: 8

      launch_template:
        id: ${aws_launch_template.app.id}
        version: $Latest

      instance_refresh:
        strategy: Rolling
        preferences:
          min_healthy_percentage: 75
          instance_warmup: 300
          checkpoint_delay: 600
          checkpoint_percentages:
            - 25
            - 50
            - 100
        triggers:
          - tag
```

### Warm Pool

```yaml
resource:
  aws_autoscaling_group:
    app:
      name: app-asg
      vpc_zone_identifier:
        - ${aws_subnet.private_a.id}
        - ${aws_subnet.private_b.id}
      desired_capacity: 2
      min_size: 1
      max_size: 10

      launch_template:
        id: ${aws_launch_template.app.id}
        version: $Latest

      warm_pool:
        pool_state: Stopped
        min_size: 2
        max_group_prepared_capacity: 5

        instance_reuse_policy:
          reuse_on_scale_in: true
```

## Lifecycle Hooks

```yaml
resource:
  aws_autoscaling_lifecycle_hook:
    launch:
      name: launch-hook
      autoscaling_group_name: ${aws_autoscaling_group.app.name}
      lifecycle_transition: autoscaling:EC2_INSTANCE_LAUNCHING
      default_result: CONTINUE
      heartbeat_timeout: 300
      notification_target_arn: ${aws_sns_topic.lifecycle.arn}
      role_arn: ${aws_iam_role.lifecycle.arn}

    terminate:
      name: terminate-hook
      autoscaling_group_name: ${aws_autoscaling_group.app.name}
      lifecycle_transition: autoscaling:EC2_INSTANCE_TERMINATING
      default_result: CONTINUE
      heartbeat_timeout: 300
```

## Attributes Reference

| Attribute | Description |
|-----------|-------------|
| id | ASG ID |
| arn | ASG ARN |
| name | ASG name |
| availability_zones | AZs in use |

## Best Practices

- **Use multiple AZs** for high availability
- **Set appropriate health check grace period**
- **Use ELB health checks** with load balancers
- **Implement instance refresh** for safe updates
- **Use target tracking** for simple scaling
- **Consider warm pools** for faster scaling
- **Tag instances** for identification
- **Monitor scaling activities**

## Scaling Policy Comparison

| Policy Type | Use Case |
|-------------|----------|
| Target Tracking | Maintain specific metric value |
| Step Scaling | Different actions for different thresholds |
| Simple Scaling | Basic up/down adjustments |
| Scheduled | Predictable traffic patterns |
| Predictive | ML-based forecasting |

## Related Resources

- [Launch Template](launch-template.md)
- [EC2 Instance](ec2-instance.md)
- [Load Balancer](../networking/load-balancer.md)
- [CloudWatch](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm)
