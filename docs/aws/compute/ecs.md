# ECS (Elastic Container Service)

Deploy and manage containerized applications with Amazon ECS using ytofu YAML.

## Basic ECS Service with Load Balancer

```yaml
resource:
  aws_ecs_service:
    mongo:
      name: mongodb
      cluster: ${aws_ecs_cluster.foo.id}
      task_definition: ${aws_ecs_task_definition.mongo.arn}
      desired_count: 3
      iam_role: ${aws_iam_role.foo.arn}
      depends_on:
        - aws_iam_role_policy.foo
      ordered_placement_strategy:
        - type: binpack
          field: cpu
      load_balancer:
        - target_group_arn: ${aws_lb_target_group.foo.arn}
          container_name: mongo
          container_port: 8080
      placement_constraints:
        - type: memberOf
          expression: "attribute:ecs.availability-zone in [us-west-2a, us-west-2b]"
```

## Daemon Scheduling Strategy

```yaml
resource:
  aws_ecs_service:
    bar:
      name: bar
      cluster: ${aws_ecs_cluster.foo.id}
      task_definition: ${aws_ecs_task_definition.bar.arn}
      scheduling_strategy: DAEMON
```

## CloudWatch Deployment Alarms

```yaml
resource:
  aws_ecs_service:
    example:
      name: example
      cluster: ${aws_ecs_cluster.example.id}
      alarms:
        enable: true
        rollback: true
        alarm_names:
          - ${aws_cloudwatch_metric_alarm.example.alarm_name}
```

## External Deployment Controller

```yaml
resource:
  aws_ecs_service:
    example:
      name: example
      cluster: ${aws_ecs_cluster.example.id}
      deployment_controller:
        type: EXTERNAL
```

## Blue/Green Deployment

```yaml
resource:
  aws_ecs_service:
    example:
      name: example
      cluster: ${aws_ecs_cluster.example.id}
      task_definition: ${aws_ecs_task_definition.example.arn}
      desired_count: 2
      deployment_configuration:
        strategy: BLUE_GREEN
      sigint_rollback: true
      wait_for_steady_state: true
```

## Linear Deployment Strategy

```yaml
resource:
  aws_ecs_service:
    example:
      name: example
      cluster: ${aws_ecs_cluster.example.id}
      task_definition: ${aws_ecs_task_definition.example.arn}
      desired_count: 4
      deployment_configuration:
        strategy: LINEAR
        bake_time_in_minutes: 10
        linear_configuration:
          step_percent: 25.0
          step_bake_time_in_minutes: 5
```

## Canary Deployment Strategy

```yaml
resource:
  aws_ecs_service:
    example:
      name: example
      cluster: ${aws_ecs_cluster.example.id}
      task_definition: ${aws_ecs_task_definition.example.arn}
      desired_count: 4
      deployment_configuration:
        strategy: CANARY
        bake_time_in_minutes: 15
        canary_configuration:
          canary_percent: 10.0
          canary_bake_time_in_minutes: 5
```

## Redeploy Service On Every Apply

```yaml
resource:
  aws_ecs_service:
    example:
      name: example
      cluster: ${aws_ecs_cluster.example.id}
      task_definition: ${aws_ecs_task_definition.example.arn}
      force_new_deployment: true
      triggers:
        redeployment: ${plantimestamp()}
```

## Ignoring Changes to Desired Count

```yaml
resource:
  aws_ecs_service:
    example:
      name: example
      cluster: ${aws_ecs_cluster.example.id}
      task_definition: ${aws_ecs_task_definition.example.arn}
      desired_count: 2
      lifecycle:
        ignore_changes:
          - desired_count
```

## Complete Fargate Service

```yaml
resource:
  # ECS Cluster
  aws_ecs_cluster:
    main:
      name: my-cluster

  # Task Definition
  aws_ecs_task_definition:
    app:
      family: my-app
      network_mode: awsvpc
      requires_compatibilities:
        - FARGATE
      cpu: "256"
      memory: "512"
      execution_role_arn: ${aws_iam_role.ecs_execution.arn}
      task_role_arn: ${aws_iam_role.ecs_task.arn}
      container_definitions: |
        [
          {
            "name": "app",
            "image": "nginx:latest",
            "portMappings": [
              {
                "containerPort": 80,
                "hostPort": 80,
                "protocol": "tcp"
              }
            ],
            "essential": true,
            "logConfiguration": {
              "logDriver": "awslogs",
              "options": {
                "awslogs-group": "/ecs/my-app",
                "awslogs-region": "us-west-2",
                "awslogs-stream-prefix": "ecs"
              }
            }
          }
        ]

  # ECS Service
  aws_ecs_service:
    app:
      name: my-app
      cluster: ${aws_ecs_cluster.main.id}
      task_definition: ${aws_ecs_task_definition.app.arn}
      desired_count: 2
      launch_type: FARGATE
      network_configuration:
        subnets:
          - ${aws_subnet.private_a.id}
          - ${aws_subnet.private_b.id}
        security_groups:
          - ${aws_security_group.ecs.id}
        assign_public_ip: false
      load_balancer:
        - target_group_arn: ${aws_lb_target_group.app.arn}
          container_name: app
          container_port: 80
```

## Arguments Reference (Cluster)

| Argument | Type | Required | Description |
|----------|------|----------|-------------|
| name | string | Yes | Cluster name |
| setting | list | No | Cluster settings |
| configuration | object | No | Execute command config |
| tags | map | No | Resource tags |

## Arguments Reference (Task Definition)

| Argument | Type | Required | Description |
|----------|------|----------|-------------|
| family | string | Yes | Task family name |
| container_definitions | string | Yes | JSON container definitions |
| network_mode | string | No | awsvpc, bridge, host, none |
| requires_compatibilities | list | No | FARGATE, EC2 |
| cpu | string | No | Task CPU (Fargate required) |
| memory | string | No | Task memory (Fargate required) |
| execution_role_arn | string | No | Execution role ARN |
| task_role_arn | string | No | Task role ARN |

## Arguments Reference (Service)

| Argument | Type | Required | Description |
|----------|------|----------|-------------|
| name | string | Yes | Service name |
| cluster | string | Yes | Cluster ID |
| task_definition | string | Yes | Task definition ARN |
| desired_count | number | No | Number of tasks |
| launch_type | string | No | FARGATE or EC2 |
| scheduling_strategy | string | No | REPLICA or DAEMON |
| network_configuration | object | No | VPC configuration |
| load_balancer | list | No | Load balancer config |
| deployment_configuration | object | No | Deployment strategy |
| force_new_deployment | bool | No | Force redeploy |

## IAM Roles for ECS

```yaml
resource:
  # Execution Role (for ECS agent)
  aws_iam_role:
    ecs_execution:
      name: ecs-execution-role
      assume_role_policy: |
        {
          "Version": "2012-10-17",
          "Statement": [{
            "Action": "sts:AssumeRole",
            "Principal": {"Service": "ecs-tasks.amazonaws.com"},
            "Effect": "Allow"
          }]
        }

  aws_iam_role_policy_attachment:
    ecs_execution:
      role: ${aws_iam_role.ecs_execution.name}
      policy_arn: arn:aws:iam::aws:policy/service-role/AmazonECSTaskExecutionRolePolicy

  # Task Role (for application)
  aws_iam_role:
    ecs_task:
      name: ecs-task-role
      assume_role_policy: |
        {
          "Version": "2012-10-17",
          "Statement": [{
            "Action": "sts:AssumeRole",
            "Principal": {"Service": "ecs-tasks.amazonaws.com"},
            "Effect": "Allow"
          }]
        }
```

## Auto Scaling

```yaml
resource:
  aws_appautoscaling_target:
    ecs:
      max_capacity: 10
      min_capacity: 2
      resource_id: service/${aws_ecs_cluster.main.name}/${aws_ecs_service.app.name}
      scalable_dimension: ecs:service:DesiredCount
      service_namespace: ecs

  aws_appautoscaling_policy:
    cpu:
      name: cpu-scaling
      policy_type: TargetTrackingScaling
      resource_id: ${aws_appautoscaling_target.ecs.resource_id}
      scalable_dimension: ${aws_appautoscaling_target.ecs.scalable_dimension}
      service_namespace: ${aws_appautoscaling_target.ecs.service_namespace}
      target_tracking_scaling_policy_configuration:
        predefined_metric_specification:
          predefined_metric_type: ECSServiceAverageCPUUtilization
        target_value: 70
        scale_in_cooldown: 300
        scale_out_cooldown: 60
```

## Fargate CPU/Memory Combinations

| CPU | Memory Options |
|-----|----------------|
| 256 | 512, 1024, 2048 |
| 512 | 1024-4096 (1GB increments) |
| 1024 | 2048-8192 (1GB increments) |
| 2048 | 4096-16384 (1GB increments) |
| 4096 | 8192-30720 (1GB increments) |

## Attributes Reference

| Attribute | Description |
|-----------|-------------|
| cluster.id | Cluster ID |
| cluster.arn | Cluster ARN |
| task_definition.arn | Task definition ARN |
| task_definition.revision | Task definition revision |
| service.id | Service ID |

## Best Practices

- **Use Fargate** for simpler operations
- **Define resource limits** in container definitions
- **Use secrets manager** for sensitive data
- **Enable CloudWatch logging** for debugging
- **Use service discovery** for service-to-service communication
- **Implement health checks** properly
- **Use deployment strategies** for zero-downtime updates
- **Use ignore_changes** for desired_count when using auto scaling

## Related Resources

- [Load Balancer](../networking/load-balancer.md)
- [Security Groups](../networking/security-groups.md)
- [VPC](../networking/vpc.md)
- [Lambda](lambda.md)
