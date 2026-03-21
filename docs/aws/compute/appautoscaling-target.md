# Appautoscaling Target

Manage Appautoscaling Target resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appautoscaling_target:
    dynamodb_table_read_target:
      max_capacity: 100
      min_capacity: 5
      resource_id: "table/${aws_dynamodb_table.example.name}"
      scalable_dimension: "dynamodb:table:ReadCapacityUnits"
      service_namespace: dynamodb
```

## DynamoDB Index Autoscaling

```yaml
resource:
  aws_appautoscaling_target:
    dynamodb_index_read_target:
      max_capacity: 100
      min_capacity: 5
      resource_id: "table/${aws_dynamodb_table.example.name}/index/example-index_name"
      scalable_dimension: "dynamodb:index:ReadCapacityUnits"
      service_namespace: dynamodb
```

## ECS Service Autoscaling

```yaml
resource:
  aws_appautoscaling_target:
    ecs_target:
      max_capacity: 4
      min_capacity: 1
      resource_id: "service/${aws_ecs_cluster.example.name}/${aws_ecs_service.example.name}"
      scalable_dimension: "ecs:service:DesiredCount"
      service_namespace: ecs
```

## Aurora Read Replica Autoscaling

```yaml
resource:
  aws_appautoscaling_target:
    replicas:
      service_namespace: rds
      scalable_dimension: "rds:cluster:ReadReplicaCount"
      resource_id: "cluster:${aws_rds_cluster.example.id}"
      min_capacity: 1
      max_capacity: 15
```

## Suppressing `tags_all` Differences For Older Resources

```yaml
resource:
  aws_appautoscaling_target:
    ecs_target:
      max_capacity: 4
      min_capacity: 1
      resource_id: "service/${aws_ecs_cluster.example.name}/${aws_ecs_service.example.name}"
      scalable_dimension: "ecs:service:DesiredCount"
      service_namespace: ecs
      lifecycle:
        ignore_changes:
          - tags_all
```
