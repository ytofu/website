# Arcregionswitch Plan

Manage Arcregionswitch Plan resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iam_role:
    example:
      name: arc-region-switch-role
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": "sts:AssumeRole" "Effect": "Allow" "Principal": { "Service": "arc-region-switch.amazonaws.com" } }, ] }'

resource:
  aws_arcregionswitch_plan:
    example:
      name: example-plan
      execution_role: ${aws_iam_role.example.arn}
      recovery_approach: activePassive
      regions: 
        - us-east-1
        - us-west-2
      primary_region: us-east-1
      workflow:
        workflow_target_action: activate
        workflow_target_region: us-west-2
        step:
          name: manual-approval
          execution_block_type: ManualApproval
          execution_approval_config:
            approval_role: ${aws_iam_role.example.arn}
            timeout_minutes: 60
      workflow:
        workflow_target_action: deactivate
        workflow_target_region: us-east-1
        step:
          name: manual-approval
          execution_block_type: ManualApproval
          execution_approval_config:
            approval_role: ${aws_iam_role.example.arn}
            timeout_minutes: 60
```

## Complex Usage with Multiple Step Types

```yaml
resource:
  aws_arcregionswitch_plan:
    complex:
      name: complex-plan
      execution_role: ${aws_iam_role.example.arn}
      recovery_approach: activeActive
      regions: 
        - us-east-1
        - us-west-2
      description: Complex plan with multiple execution block types
      recovery_time_objective_minutes: 60
      associated_alarms:
        name: application-health-alarm
        alarm_type: applicationHealth
        resource_identifier: "arn:aws:cloudwatch:us-east-1:123456789012:alarm:MyAlarm"
      workflow:
        workflow_target_action: activate
        workflow_target_region: us-west-2
        step:
          name: lambda-step
          execution_block_type: CustomActionLambda
          custom_action_lambda_config:
            region_to_run: activatingRegion
            retry_interval_minutes: 5.0
            timeout_minutes: 30
            lambda:
              arn: ${aws_lambda_function.example.arn}
        step:
          name: parallel-step
          execution_block_type: Parallel
          parallel_config:
            step:
              name: asg-scaling
              execution_block_type: EC2AutoScaling
              ec2_asg_capacity_increase_config:
                asg:
                  arn: ${aws_autoscaling_group.example.arn}
                target_percent: 150
            step:
              name: ecs-scaling
              execution_block_type: ECSServiceScaling
              ecs_capacity_increase_config:
                service:
                  cluster_arn: ${aws_ecs_cluster.example.arn}
                  service_arn: ${aws_ecs_service.example.arn}
                target_percent: 200
      workflow:
        workflow_target_action: deactivate
        workflow_target_region: us-east-1
        step:
          name: route53-health-check
          execution_block_type: Route53HealthCheck
          route53_health_check_config:
            hosted_zone_id: ${aws_route53_zone.example.zone_id}
            record_name: api.example.com
      triggers:
        action: activate
        target_region: us-west-2
        min_delay_minutes_between_executions: 30
        conditions:
          associated_alarm_name: application-health-alarm
          condition: red
      tags:
        Environment: production
```
