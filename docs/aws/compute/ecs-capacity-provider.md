# ECS Capacity Provider

Manage ECS Capacity Provider resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_autoscaling_group:
    example:
      tag:
        key: AmazonECSManaged
        value: true
        propagate_at_launch: true

resource:
  aws_ecs_capacity_provider:
    example:
      name: example
      auto_scaling_group_provider:
        auto_scaling_group_arn: ${aws_autoscaling_group.example.arn}
        managed_termination_protection: ENABLED
        managed_scaling:
          maximum_scaling_step_size: 1000
          minimum_scaling_step_size: 1
          status: ENABLED
          target_capacity: 10
```

## Managed Instances Provider

```yaml
resource:
  aws_ecs_capacity_provider:
    example:
      name: example
      cluster: my-cluster
      managed_instances_provider:
        infrastructure_role_arn: ${aws_iam_role.ecs_infrastructure.arn}
        propagate_tags: CAPACITY_PROVIDER
        instance_launch_template:
          ec2_instance_profile_arn: ${aws_iam_instance_profile.ecs_instance.arn}
          monitoring: ENABLED
          network_configuration:
            subnets: 
              - ${aws_subnet.example.id}
            security_groups: 
              - ${aws_security_group.example.id}
          storage_configuration:
            storage_size_gib: 30
          instance_requirements:
            memory_mib:
              min: 1024
              max: 8192
            vcpu_count:
              min: 1
              max: 4
            instance_generations: 
              - current
            cpu_manufacturers: 
              - intel
              - amd
```
