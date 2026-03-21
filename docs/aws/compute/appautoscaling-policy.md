# Appautoscaling Policy

Manage Appautoscaling Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appautoscaling_target:
    dynamodb_table_read_target:
      max_capacity: 100
      min_capacity: 5
      resource_id: table/tableName
      scalable_dimension: "dynamodb:table:ReadCapacityUnits"
      service_namespace: dynamodb

resource:
  aws_appautoscaling_policy:
    dynamodb_table_read_policy:
      name: "DynamoDBReadCapacityUtilization:${aws_appautoscaling_target.dynamodb_table_read_target.resource_id}"
      policy_type: TargetTrackingScaling
      resource_id: ${aws_appautoscaling_target.dynamodb_table_read_target.resource_id}
      scalable_dimension: ${aws_appautoscaling_target.dynamodb_table_read_target.scalable_dimension}
      service_namespace: ${aws_appautoscaling_target.dynamodb_table_read_target.service_namespace}
      target_tracking_scaling_policy_configuration:
        predefined_metric_specification:
          predefined_metric_type: DynamoDBReadCapacityUtilization
        target_value: 70
```

## ECS Service Autoscaling

```yaml
resource:
  aws_appautoscaling_target:
    ecs_target:
      max_capacity: 4
      min_capacity: 1
      resource_id: service/clusterName/serviceName
      scalable_dimension: "ecs:service:DesiredCount"
      service_namespace: ecs

resource:
  aws_appautoscaling_policy:
    ecs_policy:
      name: scale-down
      policy_type: StepScaling
      resource_id: ${aws_appautoscaling_target.ecs_target.resource_id}
      scalable_dimension: ${aws_appautoscaling_target.ecs_target.scalable_dimension}
      service_namespace: ${aws_appautoscaling_target.ecs_target.service_namespace}
      step_scaling_policy_configuration:
        adjustment_type: ChangeInCapacity
        cooldown: 60
        metric_aggregation_type: Maximum
        step_adjustment:
          metric_interval_upper_bound: 0
          scaling_adjustment: -1
```

## Preserve desired count when updating an autoscaled ECS Service

```yaml
resource:
  aws_ecs_service:
    ecs_service:
      name: serviceName
      cluster: clusterName
      task_definition: "taskDefinitionFamily:1"
      desired_count: 2
      lifecycle:
        ignore_changes: 
          - desired_count
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

resource:
  aws_appautoscaling_policy:
    replicas:
      name: cpu-auto-scaling
      service_namespace: ${aws_appautoscaling_target.replicas.service_namespace}
      scalable_dimension: ${aws_appautoscaling_target.replicas.scalable_dimension}
      resource_id: ${aws_appautoscaling_target.replicas.resource_id}
      policy_type: TargetTrackingScaling
      target_tracking_scaling_policy_configuration:
        predefined_metric_specification:
          predefined_metric_type: RDSReaderAverageCPUUtilization
        target_value: 75
        scale_in_cooldown: 300
        scale_out_cooldown: 300
```

## Create target tracking scaling policy using metric math

```yaml
resource:
  aws_appautoscaling_target:
    ecs_target:
      max_capacity: 4
      min_capacity: 1
      resource_id: service/clusterName/serviceName
      scalable_dimension: "ecs:service:DesiredCount"
      service_namespace: ecs

resource:
  aws_appautoscaling_policy:
    example:
      name: foo
      policy_type: TargetTrackingScaling
      resource_id: ${aws_appautoscaling_target.ecs_target.resource_id}
      scalable_dimension: ${aws_appautoscaling_target.ecs_target.scalable_dimension}
      service_namespace: ${aws_appautoscaling_target.ecs_target.service_namespace}
      target_tracking_scaling_policy_configuration:
        target_value: 100
        customized_metric_specification:
          metrics:
            label: Get the queue size (the number of messages waiting to be processed)
            id: m1
            metric_stat:
              metric:
                metric_name: ApproximateNumberOfMessagesVisible
                namespace: AWS/SQS
                dimensions:
                  name: QueueName
                  value: my-queue
              stat: Sum
            return_data: false
          metrics:
            label: Get the ECS running task count (the number of currently running tasks)
            id: m2
            metric_stat:
              metric:
                metric_name: RunningTaskCount
                namespace: ECS/ContainerInsights
                dimensions:
                  name: ClusterName
                  value: default
                dimensions:
                  name: ServiceName
                  value: web-app
              stat: Average
            return_data: false
          metrics:
            label: Calculate the backlog per instance
            id: e1
            expression: m1 / m2
            return_data: true
```

## Predictive Scaling

```yaml
resource:
  aws_appautoscaling_policy:
    example:
      name: example-policy
      resource_id: ${aws_appautoscaling_target.example.resource_id}
      scalable_dimension: ${aws_appautoscaling_target.example.scalable_dimension}
      service_namespace: ${aws_appautoscaling_target.example.service_namespace}
      policy_type: PredictiveScaling
      predictive_scaling_policy_configuration:
        metric_specification:
          target_value: 40
          predefined_metric_pair_specification:
            predefined_metric_type: ECSServiceMemoryUtilization
```
