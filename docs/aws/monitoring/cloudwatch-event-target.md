# CloudWatch Event Target

Attach targets to EventBridge rules using ytofu YAML.

## Lambda Target

```yaml
resource:
  aws_cloudwatch_event_target:
    lambda:
      rule: ${aws_cloudwatch_event_rule.every_hour.name}
      target_id: RunLambda
      arn: ${aws_lambda_function.example.arn}
```

## SNS Target

```yaml
resource:
  aws_cloudwatch_event_target:
    sns:
      rule: ${aws_cloudwatch_event_rule.ec2_state.name}
      target_id: SendToSNS
      arn: ${aws_sns_topic.alerts.arn}
```

## SQS Target

```yaml
resource:
  aws_cloudwatch_event_target:
    sqs:
      rule: ${aws_cloudwatch_event_rule.example.name}
      target_id: SendToSQS
      arn: ${aws_sqs_queue.example.arn}
```

## ECS Task Target

```yaml
resource:
  aws_cloudwatch_event_target:
    ecs:
      rule: ${aws_cloudwatch_event_rule.every_hour.name}
      target_id: RunECSTask
      arn: ${aws_ecs_cluster.example.arn}
      role_arn: ${aws_iam_role.ecs_events.arn}
      ecs_target:
        task_count: 1
        task_definition_arn: ${aws_ecs_task_definition.example.arn}
        launch_type: FARGATE
        network_configuration:
          subnets:
            - ${aws_subnet.private.id}
          security_groups:
            - ${aws_security_group.ecs.id}
```
