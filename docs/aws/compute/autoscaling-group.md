# Resource: aws_autoscaling_group

Provides an Auto Scaling Group resource.

## Basic Example

```yaml
resource:
  aws_placement_group:
    test:
      name: test
      strategy: cluster

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
        propagate_at_launch: false```

## With Latest Version Of Launch Template

```yaml
resource:
  aws_launch_template:
    foobar:
      name_prefix: foobar
      image_id: ami-1a2b3c
      instance_type: t2.micro

  aws_autoscaling_group:
    bar:
      availability_zones: 
        - us-east-1a
      desired_capacity: 1
      max_size: 1
      min_size: 1
      launch_template:
        id: ${aws_launch_template.foobar.id}
        version: $Latest```

## Mixed Instances Policy

```yaml
resource:
  aws_launch_template:
    example:
      name_prefix: example
      image_id: ${data.aws_ami.example.id}
      instance_type: c5.large

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
            weighted_capacity: 2```

## Mixed Instances Policy with Spot Instances and Capacity Rebalance

```yaml
resource:
  aws_launch_template:
    example:
      name_prefix: example
      image_id: ${data.aws_ami.example.id}
      instance_type: c5.large

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
            weighted_capacity: 2```

## Mixed Instances Policy with Instance level LaunchTemplateSpecification Overrides

```yaml
resource:
  aws_launch_template:
    example:
      name_prefix: example
      image_id: ${data.aws_ami.example.id}
      instance_type: c5.large

  aws_launch_template:
    example2:
      name_prefix: example2
      image_id: ${data.aws_ami.example2.id}

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
            weighted_capacity: 2```

## Mixed Instances Policy with Attribute-based Instance Type Selection

```yaml
resource:
  aws_launch_template:
    example:
      name_prefix: example
      image_id: ${data.aws_ami.example.id}
      instance_type: c5.large

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
                min: 4```

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

  aws_launch_template:
    example:
      image_id: ${data.aws_ami.example.id}
      instance_type: t3.nano

data:
  aws_ami:
    example:
      most_recent: true
      owners: 
        - amazon
      filter:
        name: name
        values: 
          - "amzn-ami-hvm-*-x86_64-gp2"```

## Auto Scaling group with Warm Pool

```yaml
resource:
  aws_launch_template:
    example:
      name_prefix: example
      image_id: ${data.aws_ami.example.id}
      instance_type: c5.large

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
          reuse_on_scale_in: true```

## Auto Scaling group with Traffic Sources

```yaml
resource:
  aws_autoscaling_group:
    test:
      vpc_zone_identifier: ${aws_subnet.test.id}
      max_size: 1
      min_size: 1
      force_delete: true```

## Argument Reference

This resource supports the following arguments:

- `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
- `name` - (Optional) Name of the Auto Scaling Group. By default generated by ytofu. Conflicts with `name_prefix`.
- `name_prefix` - (Optional) Creates a unique name beginning with the specified
  prefix. Conflicts with `name`.
- `max_size` - (Required) Maximum size of the Auto Scaling Group.
- `min_size` - (Required) Minimum size of the Auto Scaling Group.
  (See also [Waiting for Capacity](#waiting-for-capacity) below.)
- `availability_zones` - (Optional) A list of Availability Zones where instances in the Auto Scaling group can be created. Used for launching into the default VPC subnet in each Availability Zone when not using the `vpc_zone_identifier` attribute, or for attaching a network interface when an existing network interface ID is specified in a launch template. Conflicts with `vpc_zone_identifier`.
- `availability_zone_distribution` (Optional) The instance capacity distribution across Availability Zones. See [Availability Zone Distribution](#availability_zone_distribution) below for more details.
- `capacity_reservation_specification` (Optional) The capacity reservation specification for the Auto Scaling group allows you to prioritize launching into On-Demand Capacity Reservations. See [Capacity Reservation Specification](#capacity_reservation_specification) below for more details.
- `capacity_rebalance` - (Optional) Whether capacity rebalance is enabled. Otherwise, capacity rebalance is disabled.
- `context` - (Optional) Reserved.
- `default_cooldown` - (Optional) Amount of time, in seconds, after a scaling activity completes before another scaling activity can start.
- `default_instance_warmup` - (Optional) Amount of time, in seconds, until a newly launched instance can contribute to the Amazon CloudWatch metrics. This delay lets an instance finish initializing before Amazon EC2 Auto Scaling aggregates instance metrics, resulting in more reliable usage data. Set this value equal to the amount of time that it takes for resource consumption to become stable after an instance reaches the InService state. (See [Set the default instance warmup for an Auto Scaling group](https://docs.aws.amazon.com/autoscaling/ec2/userguide/ec2-auto-scaling-default-instance-warmup.html))
- `launch_configuration` - (Optional) Name of the launch configuration to use.
- `launch_template` - (Optional) Nested argument with Launch template specification to use to launch instances. See [Launch Template](#launch_template) below for more details.
- `mixed_instances_policy` - (Optional) Configuration block containing settings to define launch targets for Auto Scaling groups. See [Mixed Instances Policy](#mixed_instances_policy) below for more details.
- `ignore_failed_scaling_activities` - (Optional) Whether to ignore failed [Auto Scaling scaling activities](https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-verify-scaling-activity.html) while [waiting for capacity](#waiting-for-capacity). The default is `false` -- failed scaling activities cause errors to be returned.
- `initial_lifecycle_hook` - (Optional) One or more
  [Lifecycle Hooks](http://docs.aws.amazon.com/autoscaling/latest/userguide/lifecycle-hooks.html)
  to attach to the Auto Scaling Group **before** instances are launched. The
  syntax is exactly the same as the separate
  `aws_autoscaling_lifecycle_hook`
  resource, without the `autoscaling_group_name` attribute. Please note that this will only work when creating
  a new Auto Scaling Group. For all other use-cases, please use `aws_autoscaling_lifecycle_hook` resource.
- `health_check_grace_period` - (Optional, Default: 300) Time (in seconds) after instance comes into service before checking health.
- `health_check_type` - (Optional) "EC2" or "ELB". Controls how health checking is done.
- `instance_maintenance_policy` - (Optional) If this block is configured, add a instance maintenance policy to the specified Auto Scaling group. Defined [below](#instance_maintenance_policy).
- `desired_capacity` - (Optional) Number of Amazon EC2 instances that
  should be running in the group. (See also [Waiting for
  Capacity](#waiting-for-capacity) below.)
- `desired_capacity_type` - (Optional) The unit of measurement for the value specified for `desired_capacity`. Supported for attribute-based instance type selection only. Valid values: `"units"`, `"vcpu"`, `"memory-mib"`.
- `force_delete` - (Optional) Allows deleting the Auto Scaling Group without waiting
  for all instances in the pool to terminate. You can force an Auto Scaling Group to delete
  even if it's in the process of scaling a resource. Normally, ytofu
  drains all the instances before deleting the group. This bypasses that
  behavior and potentially leaves resources dangling.
- `load_balancers` - (Optional) List of elastic load balancer names to add to the autoscaling
  group names. Only valid for classic load balancers. For ALBs, use `target_group_arns` instead. To remove all load balancer attachments an empty list should be specified.
- `traffic_source` - (Optional) Attaches one or more traffic sources to the specified Auto Scaling group.
- `vpc_zone_identifier` - (Optional) List of subnet IDs to launch resources in. Subnets automatically determine which availability zones the group will reside. Conflicts with `availability_zones`.
- `target_group_arns` - (Optional) Set of `aws_lb_target_group` ARNs, for use with Application or Network Load Balancing. To remove all target group attachments an empty list should be specified.
- `termination_policies` - (Optional) List of policies to decide how the instances in the Auto Scaling Group should be terminated. The allowed values are `OldestInstance`, `NewestInstance`, `OldestLaunchConfiguration`, `ClosestToNextInstanceHour`, `OldestLaunchTemplate`, `AllocationStrategy`, `Default`. Additionally, the ARN of a Lambda function can be specified for custom termination policies.
- `suspended_processes` - (Optional) List of processes to suspend for the Auto Scaling Group. The allowed values are `Launch`, `Terminate`, `HealthCheck`, `ReplaceUnhealthy`, `AZRebalance`, `AlarmNotification`, `ScheduledActions`, `AddToLoadBalancer`, `InstanceRefresh`.
  Note that if you suspend either the `Launch` or `Terminate` process types, it can prevent your Auto Scaling Group from functioning properly.
- `tag` - (Optional) Configuration block(s) containing resource tags. See [Tag](#tag) below for more details.
- `placement_group` - (Optional) Name of the placement group into which you'll launch your instances, if any.
- `metrics_granularity` - (Optional) Granularity to associate with the metrics to collect. The only valid value is `1Minute`. Default is `1Minute`.
- `enabled_metrics` - (Optional) List of metrics to collect. The allowed values are defined by the [underlying AWS API](https://docs.aws.amazon.com/autoscaling/ec2/APIReference/API_EnableMetricsCollection.html).
- `wait_for_capacity_timeout` - (Optional, Default: "10m") Maximum
  [duration](https://golang.org/pkg/time/#ParseDuration) that ytofu should
  wait for ASG instances to be healthy before timing out. (See also [Waiting
  for Capacity](#waiting-for-capacity) below.) Setting this to "0" causes
  ytofu to skip all Capacity Waiting behavior.
- `min_elb_capacity` - (Optional) Setting this causes ytofu to wait for
  this number of instances from this Auto Scaling Group to show up healthy in the
  ELB only on creation. Updates will not wait on ELB instance number changes.
  (See also [Waiting for Capacity](#waiting-for-capacity) below.)
- `wait_for_elb_capacity` - (Optional) Setting this will cause ytofu to wait
  for exactly this number of healthy instances from this Auto Scaling Group in
  all attached load balancers on both create and update operations. (Takes
  precedence over `min_elb_capacity` behavior.)
  (See also [Waiting for Capacity](#waiting-for-capacity) below.)
- `protect_from_scale_in` - (Optional) Whether newly launched instances
  are automatically protected from termination by Amazon EC2 Auto Scaling when
  scaling in. For more information about preventing instances from terminating
  on scale in, see [Using instance scale-in protection](https://docs.aws.amazon.com/autoscaling/ec2/userguide/ec2-auto-scaling-instance-protection.html)
  in the Amazon EC2 Auto Scaling User Guide.
- `service_linked_role_arn` - (Optional) ARN of the service-linked role that the ASG will use to call other AWS services
- `max_instance_lifetime` - (Optional) Maximum amount of time, in seconds, that an instance can be in service, values must be either equal to 0 or between 86400 and 31536000 seconds.
- `instance_refresh` - (Optional) If this block is configured, start an
  [Instance Refresh](https://docs.aws.amazon.com/autoscaling/ec2/userguide/asg-instance-refresh.html)
  when this Auto Scaling Group is updated. Defined [below](#instance_refresh).
- `warm_pool` - (Optional) If this block is configured, add a [Warm Pool](https://docs.aws.amazon.com/autoscaling/ec2/userguide/ec2-auto-scaling-warm-pools.html)
  to the specified Auto Scaling group. Defined [below](#warm_pool)
- `force_delete_warm_pool` - (Optional) Allows deleting the Auto Scaling Group without waiting for all instances in the warm pool to terminate.

### availability_zone_distribution

- `capacity_distribution_strategy` - (Required) The strategy to use for distributing capacity across the Availability Zones. Valid values are `balanced-only` and `balanced-best-effort`. Default is `balanced-best-effort`.

### capacity_reservation_specification

- `capacity_reservation_preference` - (Required) Capacity Reservation preference helps you use Capacity Reservations efficiently by prioritizing reserved capacity in a Capacity Reservation before using On-Demand capacity. Valid values are `default`, `capacity-reservations-only`, `capacity-reservations-first` and `none`. Default is `default`.
- `capacity_reservation_target` - (Optional) Describes a target Capacity Reservation or Capacity Reservation resource group.

#### capacity_reservation_specification capacity_reservation_target

This configuration block supports the following:

- `capacity_reservation_ids` - (Optional) List of On-Demand Capacity Reservation Ids. Conflicts with `capacity_reservation_resource_group_arns`.
- `capacity_reservation_resource_group_arns` - (Optional) List of On-Demand Capacity Reservation Resource Group Arns. Conflicts with `capacity_reservation_ids`.

### launch_template

The top-level `launch_template` block supports the following:

- `id` - (Optional) ID of the launch template. Conflicts with `name`.
- `name` - (Optional) Name of the launch template. Conflicts with `id`.
- `version` - (Optional) Template version. Can be version number, `$Latest`, or `$Default`. (Default: `$Default`).

### mixed_instances_policy

- `instances_distribution` - (Optional) Nested argument containing settings on how to mix on-demand and Spot instances in the Auto Scaling group. Defined below.
- `launch_template` - (Required) Nested argument containing launch template settings along with the overrides to specify multiple instance types and weights. Defined below.

#### mixed_instances_policy instances_distribution

This configuration block supports the following:

- `on_demand_allocation_strategy` - (Optional) Strategy to use when launching on-demand instances. Valid values: `prioritized`, `lowest-price`. Default: `prioritized`.
- `on_demand_base_capacity` - (Optional) Absolute minimum amount of desired capacity that must be fulfilled by on-demand instances. Default: `0`.
- `on_demand_percentage_above_base_capacity` - (Optional) Percentage split between on-demand and Spot instances above the base on-demand capacity. Default: `100`.
- `spot_allocation_strategy` - (Optional) How to allocate capacity across the Spot pools. Valid values: `lowest-price`, `capacity-optimized`, `capacity-optimized-prioritized`, and `price-capacity-optimized`. Default: `lowest-price`.
- `spot_instance_pools` - (Optional) Number of Spot pools per availability zone to allocate capacity. EC2 Auto Scaling selects the cheapest Spot pools and evenly allocates Spot capacity across the number of Spot pools that you specify. Only available with `spot_allocation_strategy` set to `lowest-price`. Otherwise it must be set to `0`, if it has been defined before. Default: `2`.
- `spot_max_price` - (Optional) Maximum price per unit hour that the user is willing to pay for the Spot instances. Default: an empty string which means the on-demand price.

#### mixed_instances_policy launch_template

This configuration block supports the following:

- `launch_template_specification` - (Required) Nested argument defines the Launch Template. Defined below.
- `override` - (Optional) List of nested arguments provides the ability to specify multiple instance types. This will override the same parameter in the launch template. For on-demand instances, Auto Scaling considers the order of preference of instance types to launch based on the order specified in the overrides list. Defined below.

##### mixed_instances_policy launch_template launch_template_specification

This configuration block supports the following:

- `launch_template_id` - (Optional) ID of the launch template. Conflicts with `launch_template_name`.
- `launch_template_name` - (Optional) Name of the launch template. Conflicts with `launch_template_id`.
- `version` - (Optional) Template version. Can be version number, `$Latest`, or `$Default`. (Default: `$Default`).

##### mixed_instances_policy launch_template override

This configuration block supports the following:

- `instance_type` - (Optional) Override the instance type in the Launch Template.
- `instance_requirements` - (Optional) Override the instance type in the Launch Template with instance types that satisfy the requirements.
- `launch_template_specification` - (Optional) Override the instance launch template specification in the Launch Template.
- `weighted_capacity` - (Optional) Number of capacity units, which gives the instance type a proportional weight to other instance types.

###### mixed_instances_policy launch_template override instance_requirements

This configuration block supports the following:

- `accelerator_count` - (Optional) Block describing the minimum and maximum number of accelerators (GPUs, FPGAs, or AWS Inferentia chips). Default is no minimum or maximum.
    - `min` - (Optional) Minimum.
    - `max` - (Optional) Maximum. Set to `0` to exclude instance types with accelerators.
- `accelerator_manufacturers` - (Optional) List of accelerator manufacturer names. Default is any manufacturer.

  ```
  Valid names:
    * amazon-web-services
    * amd
    * nvidia
    * xilinx
  ```

- `accelerator_names` - (Optional) List of accelerator names. Default is any acclerator.

  ```
  Valid names:
    * a100            - NVIDIA A100 GPUs
    * v100            - NVIDIA V100 GPUs
    * k80             - NVIDIA K80 GPUs
    * t4              - NVIDIA T4 GPUs
    * m60             - NVIDIA M60 GPUs
    * radeon-pro-v520 - AMD Radeon Pro V520 GPUs
    * vu9p            - Xilinx VU9P FPGAs
  ```

- `accelerator_total_memory_mib` - (Optional) Block describing the minimum and maximum total memory of the accelerators. Default is no minimum or maximum.

    - `min` - (Optional) Minimum.
    - `max` - (Optional) Maximum.

- `accelerator_types` - (Optional) List of accelerator types. Default is any accelerator type.

  ```
  Valid types:
    * fpga
    * gpu
    * inference
  ```

- `allowed_instance_types` - (Optional) List of instance types to apply your specified attributes against. All other instance types are ignored, even if they match your specified attributes. You can use strings with one or more wild cards, represented by an asterisk (\*), to allow an instance type, size, or generation. The following are examples: `m5.8xlarge`, `c5*.*`, `m5a.*`, `r*`, `*3*`. For example, if you specify `c5*`, you are allowing the entire C5 instance family, which includes all C5a and C5n instance types. If you specify `m5a.*`, you are allowing all the M5a instance types, but not the M5n instance types. Maximum of 400 entries in the list; each entry is limited to 30 characters. Default is all instance types.

  ~> **NOTE:** If you specify `allowed_instance_types`, you can't specify `excluded_instance_types`.

- `bare_metal` - (Optional) Indicate whether bare metal instace types should be `included`, `excluded`, or `required`. Default is `excluded`.
- `baseline_ebs_bandwidth_mbps` - (Optional) Block describing the minimum and maximum baseline EBS bandwidth, in Mbps. Default is no minimum or maximum.
    - `min` - (Optional) Minimum.
    - `max` - (Optional) Maximum.
- `burstable_performance` - (Optional) Indicate whether burstable performance instance types should be `included`, `excluded`, or `required`. Default is `excluded`.
- `cpu_manufacturers` (Optional) List of CPU manufacturer names. Default is any manufacturer.

  ~> **NOTE:** Don't confuse the CPU hardware manufacturer with the CPU hardware architecture. Instances will be launched with a compatible CPU architecture based on the Amazon Machine Image (AMI) that you specify in your launch template.

  ```
  Valid names:
    * amazon-web-services
    * amd
    * intel
  ```

- `excluded_instance_types` - (Optional) List of instance types to exclude. You can use strings with one or more wild cards, represented by an asterisk (\*), to exclude an instance type, size, or generation. The following are examples: `m5.8xlarge`, `c5*.*`, `m5a.*`, `r*`, `*3*`. For example, if you specify `c5*`, you are excluding the entire C5 instance family, which includes all C5a and C5n instance types. If you specify `m5a.*`, you are excluding all the M5a instance types, but not the M5n instance types. Maximum of 400 entries in the list; each entry is limited to 30 characters. Default is no excluded instance types.

  ~> **NOTE:** If you specify `excluded_instance_types`, you can't specify `allowed_instance_types`.

- `instance_generations` - (Optional) List of instance generation names. Default is any generation.

  ```
  Valid names:
    * current  - Recommended for best performance.
    * previous - For existing applications optimized for older instance types.
  ```

- `local_storage` - (Optional) Indicate whether instance types with local storage volumes are `included`, `excluded`, or `required`. Default is `included`.
- `local_storage_types` - (Optional) List of local storage type names. Default any storage type.

  ```
  Value names:
    * hdd - hard disk drive
    * ssd - solid state drive
  ```

- `max_spot_price_as_percentage_of_optimal_on_demand_price` - (Optional) The price protection threshold for Spot Instances. This is the maximum you’ll pay for a Spot Instance, expressed as a percentage higher than the cheapest M, C, or R instance type with your specified attributes. When Amazon EC2 Auto Scaling selects instance types with your attributes, we will exclude instance types whose price is higher than your threshold. The parameter accepts an integer, which Amazon EC2 Auto Scaling interprets as a percentage. To turn off price protection, specify a high value, such as 999999. Conflicts with `spot_max_price_percentage_over_lowest_price`
- `memory_gib_per_vcpu` - (Optional) Block describing the minimum and maximum amount of memory (GiB) per vCPU. Default is no minimum or maximum.
    - `min` - (Optional) Minimum. May be a decimal number, e.g. `0.5`.
    - `max` - (Optional) Maximum. May be a decimal number, e.g. `0.5`.
- `memory_mib` - (Required) Block describing the minimum and maximum amount of memory (MiB). Default is no maximum.
    - `min` - (Required) Minimum.
    - `max` - (Optional) Maximum.
- `network_bandwidth_gbps` - (Optional) Block describing the minimum and maximum amount of network bandwidth, in gigabits per second (Gbps). Default is no minimum or maximum.
    - `min` - (Optional) Minimum.
    - `max` - (Optional) Maximum.
- `network_interface_count` - (Optional) Block describing the minimum and maximum number of network interfaces. Default is no minimum or maximum.
    - `min` - (Optional) Minimum.
    - `max` - (Optional) Maximum.
- `on_demand_max_price_percentage_over_lowest_price` - (Optional) Price protection threshold for On-Demand Instances. This is the maximum you’ll pay for an On-Demand Instance, expressed as a percentage higher than the cheapest M, C, or R instance type with your specified attributes. When Amazon EC2 Auto Scaling selects instance types with your attributes, we will exclude instance types whose price is higher than your threshold. The parameter accepts an integer, which Amazon EC2 Auto Scaling interprets as a percentage. To turn off price protection, specify a high value, such as 999999. Default is 20.

  If you set DesiredCapacityType to vcpu or memory-mib, the price protection threshold is applied based on the per vCPU or per memory price instead of the per instance price.

- `require_hibernate_support` - (Optional) Indicate whether instance types must support On-Demand Instance Hibernation, either `true` or `false`. Default is `false`.
- `spot_max_price_percentage_over_lowest_price` - (Optional) Price protection threshold for Spot Instances. This is the maximum you’ll pay for a Spot Instance, expressed as a percentage higher than the cheapest M, C, or R instance type with your specified attributes. When Amazon EC2 Auto Scaling selects instance types with your attributes, we will exclude instance types whose price is higher than your threshold. The parameter accepts an integer, which Amazon EC2 Auto Scaling interprets as a percentage. To turn off price protection, specify a high value, such as 999999. Default is 100. Conflicts with `max_spot_price_as_percentage_of_optimal_on_demand_price`

  If you set DesiredCapacityType to vcpu or memory-mib, the price protection threshold is applied based on the per vCPU or per memory price instead of the per instance price.

- `total_local_storage_gb` - (Optional) Block describing the minimum and maximum total local storage (GB). Default is no minimum or maximum.
    - `min` - (Optional) Minimum. May be a decimal number, e.g. `0.5`.
    - `max` - (Optional) Maximum. May be a decimal number, e.g. `0.5`.
- `vcpu_count` - (Required) Block describing the minimum and maximum number of vCPUs. Default is no maximum.
    - `min` - (Required) Minimum.
    - `max` - (Optional) Maximum.

### tag

The `tag` attribute accepts exactly one tag declaration with the following fields:

- `key` - (Required) Key
- `value` - (Required) Value
- `propagate_at_launch` - (Required) Enables propagation of the tag to
  Amazon EC2 instances launched via this ASG

To declare multiple tags, additional `tag` blocks can be specified.

### instance_refresh

This configuration block supports the following:

- `strategy` - (Required) Strategy to use for instance refresh. The only allowed value is `Rolling`. See [StartInstanceRefresh Action](https://docs.aws.amazon.com/autoscaling/ec2/APIReference/API_StartInstanceRefresh.html#API_StartInstanceRefresh_RequestParameters) for more information.
- `preferences` - (Optional) Override default parameters for Instance Refresh.
    - `checkpoint_delay` - (Optional) Number of seconds to wait after a checkpoint. Defaults to `3600`.
    - `checkpoint_percentages` - (Optional) List of percentages for each checkpoint. Values must be unique and in ascending order. To replace all instances, the final number must be `100`.
    - `instance_warmup` - (Optional) Number of seconds until a newly launched instance is configured and ready to use. Default behavior is to use the Auto Scaling Group's health check grace period.
    - `max_healthy_percentage` - (Optional) Amount of capacity in the Auto Scaling group that can be in service and healthy, or pending, to support your workload when an instance refresh is in place, as a percentage of the desired capacity of the Auto Scaling group. Values must be between `100` and `200`, defaults to `100`.
    - `min_healthy_percentage` - (Optional) Amount of capacity in the Auto Scaling group that must remain healthy during an instance refresh to allow the operation to continue, as a percentage of the desired capacity of the Auto Scaling group. Defaults to `90`.
    - `skip_matching` - (Optional) Skip replacing instances that already have your desired configuration. Defaults to `false`.
    - `auto_rollback` - (Optional) Automatically rollback if instance refresh fails. Defaults to `false`. This option may only be set to `true` when specifying a `launch_template` or `mixed_instances_policy`.
    - `alarm_specification` - (Optional) Alarm Specification for Instance Refresh.
        - `alarms` - (Required) List of Cloudwatch alarms. If any of these alarms goes into ALARM state, Instance Refresh is failed.
    - `scale_in_protected_instances` - (Optional) Behavior when encountering instances protected from scale in are found. Available behaviors are `Refresh`, `Ignore`, and `Wait`. Default is `Ignore`.
    - `standby_instances` - (Optional) Behavior when encountering instances in the `Standby` state in are found. Available behaviors are `Terminate`, `Ignore`, and `Wait`. Default is `Ignore`.
- `triggers` - (Optional) Set of additional property names that will trigger an Instance Refresh. A refresh will always be triggered by a change in any of `launch_configuration`, `launch_template`, or `mixed_instances_policy`.

### warm_pool

This configuration block supports the following:

- `instance_reuse_policy` - (Optional) Whether instances in the Auto Scaling group can be returned to the warm pool on scale in. The default is to terminate instances in the Auto Scaling group when the group scales in.
- `max_group_prepared_capacity` - (Optional) Total maximum number of instances that are allowed to be in the warm pool or in any state except Terminated for the Auto Scaling group.
- `min_size` - (Optional) Minimum number of instances to maintain in the warm pool. This helps you to ensure that there is always a certain number of warmed instances available to handle traffic spikes. Defaults to 0 if not specified.
- `pool_state` - (Optional) Sets the instance state to transition to after the lifecycle hooks finish. Valid values are: Stopped (default), Running or Hibernated.

### instance_maintenance_policy

This configuration block supports the following:

- `min_healthy_percentage` - (Required) Specifies the lower limit on the number of instances that must be in the InService state with a healthy status during an instance replacement activity.
- `max_healthy_percentage` - (Required) Specifies the upper limit on the number of instances that are in the InService or Pending state with a healthy status during an instance replacement activity.

### traffic_source

- `identifier` - Identifies the traffic source. For Application Load Balancers, Gateway Load Balancers, Network Load Balancers, and VPC Lattice, this will be the Amazon Resource Name (ARN) for a target group in this account and Region. For Classic Load Balancers, this will be the name of the Classic Load Balancer in this account and Region.
- `type` - Provides additional context for the value of Identifier.
  The following lists the valid values:
  `elb` if `identifier` is the name of a Classic Load Balancer.
  `elbv2` if `identifier` is the ARN of an Application Load Balancer, Gateway Load Balancer, or Network Load Balancer target group.
  `vpc-lattice` if `identifier` is the ARN of a VPC Lattice target group.

##### instance_reuse_policy

This configuration block supports the following:

- `reuse_on_scale_in` - (Optional) Whether instances in the Auto Scaling group can be returned to the warm pool on scale in.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

- `id` - Auto Scaling Group id.
- `arn` - ARN for this Auto Scaling Group
- `availability_zones` - Availability zones of the Auto Scaling Group.
- `min_size` - Minimum size of the Auto Scaling Group
- `max_size` - Maximum size of the Auto Scaling Group
- `default_cooldown` - Time between a scaling activity and the succeeding scaling activity.
- `default_instance_warmup` - The duration of the default instance warmup, in seconds.
- `name` - Name of the Auto Scaling Group
- `health_check_grace_period` - Time after instance comes into service before checking health.
- `health_check_type` - "EC2" or "ELB". Controls how health checking is done.
- `desired_capacity` -The number of Amazon EC2 instances that should be running in the group.
- `launch_configuration` - The launch configuration of the Auto Scaling Group
- `predicted_capacity` - Predicted capacity of the group.
- `vpc_zone_identifier` (Optional) - The VPC zone identifier
- `warm_pool_size` - Current size of the warm pool.

## Timeouts

Configuration options:

- `delete` - (Default `10m`)

## Import

```bash
ytofu import aws_autoscaling_group.web web-asg
```
