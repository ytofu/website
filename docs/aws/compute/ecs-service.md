# ECS Service

Manage ECS Service resources using ytofu YAML.

## Basic Example

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
        - ${aws_iam_role_policy.foo}
      ordered_placement_strategy:
        type: binpack
        field: cpu
      load_balancer:
        target_group_arn: ${aws_lb_target_group.foo.arn}
        container_name: mongo
        container_port: 8080
      placement_constraints:
        type: memberOf
        expression: "attribute:ecs.availability-zone in [us-west-2a, us-west-2b]"
```

## Ignoring Changes to Desired Count

```yaml
resource:
  aws_ecs_service:
    example:
      desired_count: 2
      lifecycle:
        ignore_changes: 
          - desired_count
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

## Blue/Green Deployment with SIGINT Rollback

```yaml
resource:
  aws_ecs_service:
    example:
      name: example
      cluster: ${aws_ecs_cluster.example.id}
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
      force_new_deployment: true
      triggers:
        redeployment: ${plantimestamp()}
```

## Service Connect with Access Logs

```yaml
resource:
  aws_ecs_service:
    example:
      name: example
      cluster: ${aws_ecs_cluster.example.id}
      task_definition: ${aws_ecs_task_definition.example.arn}
      desired_count: 1
      service_connect_configuration:
        enabled: true
        namespace: ${aws_service_discovery_http_namespace.example.arn}
        log_configuration:
          log_driver: awslogs
          options: 
        access_log_configuration:
          format: TEXT
          include_query_parameters: ENABLED
        service:
          port_name: http
          discovery_name: example
          client_alias:
            dns_name: example
            port: 8080

resource:
  aws_cloudwatch_log_group:
    example:
      name: /ecs/example/service-connect

data:
  aws_region:
    current:
```
