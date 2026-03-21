# Autoscaling Group

Manage Autoscaling Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_placement_group:
    test:
      name: test
      strategy: cluster

resource:
  aws_autoscaling_group:
    bar:
      name: foobar3-terraform-test
      max_size: 5
      min_size: 2
      health_check_grace_period: 300
      health_check_type: ELB
      desired_capacity: 4
      force_delete: true
      placement_group: ${aws_placement_group.test.id}
      launch_configuration: ${aws_launch_configuration.foobar.name}
      vpc_zone_identifier: 
        - ${aws_subnet.example1.id}
        - ${aws_subnet.example2.id}
      instance_maintenance_policy:
        min_healthy_percentage: 90
        max_healthy_percentage: 120
      initial_lifecycle_hook:
        name: foobar
        default_result: CONTINUE
        heartbeat_timeout: 2000
        lifecycle_transition: "autoscaling:EC2_INSTANCE_LAUNCHING"
        notification_metadata: '{ "foo": "bar" }'
        notification_target_arn: "arn:aws:sqs:us-east-1:444455556666:queue1*"
        role_arn: "arn:aws:iam::123456789012:role/S3Access"
      tag:
        key: foo
        value: bar
        propagate_at_launch: true
      timeouts:
        delete: 15m
      tag:
        key: lorem
        value: ipsum
        propagate_at_launch: false
```

## With Latest Version Of Launch Template

```yaml
resource:
  aws_launch_template:
    foobar:
      name_prefix: foobar
      image_id: ami-1a2b3c
      instance_type: t2.micro

resource:
  aws_autoscaling_group:
    bar:
      availability_zones: 
        - us-east-1a
      desired_capacity: 1
      max_size: 1
      min_size: 1
      launch_template:
        id: ${aws_launch_template.foobar.id}
        version: $Latest
```

## Mixed Instances Policy

```yaml
resource:
  aws_launch_template:
    example:
      name_prefix: example
      image_id: ${data.aws_ami.example.id}
      instance_type: c5.large

resource:
  aws_autoscaling_group:
    example:
      availability_zones: 
        - us-east-1a
      desired_capacity: 1
      max_size: 1
      min_size: 1
      mixed_instances_policy:
        launch_template:
          launch_template_specification:
            launch_template_id: ${aws_launch_template.example.id}
          override:
            instance_type: c4.large
            weighted_capacity: 3
          override:
            instance_type: c3.large
            weighted_capacity: 2
```

## Mixed Instances Policy with Spot Instances and Capacity Rebalance

```yaml
resource:
  aws_launch_template:
    example:
      name_prefix: example
      image_id: ${data.aws_ami.example.id}
      instance_type: c5.large

resource:
  aws_autoscaling_group:
    example:
      capacity_rebalance: true
      desired_capacity: 12
      max_size: 15
      min_size: 12
      vpc_zone_identifier: 
        - ${aws_subnet.example1.id}
        - ${aws_subnet.example2.id}
      mixed_instances_policy:
        instances_distribution:
          on_demand_base_capacity: 0
          on_demand_percentage_above_base_capacity: 25
          spot_allocation_strategy: capacity-optimized
        launch_template:
          launch_template_specification:
            launch_template_id: ${aws_launch_template.example.id}
          override:
            instance_type: c4.large
            weighted_capacity: 3
          override:
            instance_type: c3.large
            weighted_capacity: 2
```

## Mixed Instances Policy with Instance level LaunchTemplateSpecification Overrides

```yaml
resource:
  aws_launch_template:
    example:
      name_prefix: example
      image_id: ${data.aws_ami.example.id}
      instance_type: c5.large

resource:
  aws_launch_template:
    example2:
      name_prefix: example2
      image_id: ${data.aws_ami.example2.id}

resource:
  aws_autoscaling_group:
    example:
      availability_zones: 
        - us-east-1a
      desired_capacity: 1
      max_size: 1
      min_size: 1
      mixed_instances_policy:
        launch_template:
          launch_template_specification:
            launch_template_id: ${aws_launch_template.example.id}
          override:
            instance_type: c4.large
            weighted_capacity: 3
          override:
            instance_type: c6g.large
            launch_template_specification:
              launch_template_id: ${aws_launch_template.example2.id}
            weighted_capacity: 2
```

## Mixed Instances Policy with Attribute-based Instance Type Selection

```yaml
resource:
  aws_launch_template:
    example:
      name_prefix: example
      image_id: ${data.aws_ami.example.id}
      instance_type: c5.large

resource:
  aws_autoscaling_group:
    example:
      availability_zones: 
        - us-east-1a
      desired_capacity: 1
      max_size: 1
      min_size: 1
      mixed_instances_policy:
        launch_template:
          launch_template_specification:
            launch_template_id: ${aws_launch_template.example.id}
          override:
            instance_requirements:
              memory_mib:
                min: 1000
              vcpu_count:
                min: 4
```

## Dynamic tagging

```yaml
resource:
  aws_autoscaling_group:
    test:
      name: foobar3-terraform-test
      max_size: 5
      min_size: 2
      launch_configuration: ${aws_launch_configuration.foobar.name}
      vpc_zone_identifier: 
        - ${aws_subnet.example1.id}
        - ${aws_subnet.example2.id}
      tag:
        key: explicit1
        value: value1
        propagate_at_launch: true
      tag:
        key: explicit2
        value: value2
        propagate_at_launch: true```

## Automatically refresh all instances after the group is updated

```yaml
resource:
  aws_autoscaling_group:
    example:
      availability_zones: 
        - us-east-1a
      desired_capacity: 1
      max_size: 2
      min_size: 1
      launch_template:
        id: ${aws_launch_template.example.id}
        version: ${aws_launch_template.example.latest_version}
      tag:
        key: Key
        value: Value
        propagate_at_launch: true
      instance_refresh:
        strategy: Rolling
        preferences:
          min_healthy_percentage: 50
        triggers: 
          - tag

data:
  aws_ami:
    example:
      most_recent: true
      owners: 
        - amazon
      filter:
        name: name
        values: 
          - "amzn-ami-hvm-*-x86_64-gp2"

resource:
  aws_launch_template:
    example:
      image_id: ${data.aws_ami.example.id}
      instance_type: t3.nano
```

## Auto Scaling group with Warm Pool

```yaml
resource:
  aws_launch_template:
    example:
      name_prefix: example
      image_id: ${data.aws_ami.example.id}
      instance_type: c5.large

resource:
  aws_autoscaling_group:
    example:
      availability_zones: 
        - us-east-1a
      desired_capacity: 1
      max_size: 5
      min_size: 1
      warm_pool:
        pool_state: Hibernated
        min_size: 1
        max_group_prepared_capacity: 10
        instance_reuse_policy:
          reuse_on_scale_in: true
```

## Auto Scaling group with Traffic Sources

```yaml
resource:
  aws_autoscaling_group:
    test:
      vpc_zone_identifier: ${aws_subnet.test.id}
      max_size: 1
      min_size: 1
      force_delete: true```
