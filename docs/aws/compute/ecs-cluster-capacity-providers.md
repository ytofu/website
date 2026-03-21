# ECS Cluster Capacity Providers

Manage ECS Cluster Capacity Providers resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ecs_cluster:
    example:
      name: my-cluster

resource:
  aws_ecs_cluster_capacity_providers:
    example:
      cluster_name: ${aws_ecs_cluster.example.name}
      capacity_providers: 
        - FARGATE
      default_capacity_provider_strategy:
        base: 1
        weight: 100
        capacity_provider: FARGATE
```
