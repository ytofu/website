# ECS Task Set

Manage ECS Task Set resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ecs_task_set:
    example:
      service: ${aws_ecs_service.example.id}
      cluster: ${aws_ecs_cluster.example.id}
      task_definition: ${aws_ecs_task_definition.example.arn}
      load_balancer:
        target_group_arn: ${aws_lb_target_group.example.arn}
        container_name: mongo
        container_port: 8080
```

## Ignoring Changes to Scale

```yaml
resource:
  aws_ecs_task_set:
    example:
      scale:
        value: 50.0
      lifecycle:
        ignore_changes: 
          - scale
```
