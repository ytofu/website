# Autoscalingplans Scaling Plan

Manage Autoscalingplans Scaling Plan resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_availability_zones:
    available:

resource:
  aws_autoscaling_group:
    example:
      name_prefix: example
      launch_configuration: ${aws_launch_configuration.example.name}
      availability_zones: 
        - ${data.aws_availability_zones.available.names[0]}
      min_size: 0
      max_size: 3
      tags:
        - key: application

resource:
  aws_autoscalingplans_scaling_plan:
    example:
      name: example-dynamic-cost-optimization
      application_source:
        tag_filter:
          key: application
          values: 
            - example
      scaling_instruction:
        max_capacity: 3
        min_capacity: 0
        resource_id: example-formatted
        scalable_dimension: "autoscaling:autoScalingGroup:DesiredCapacity"
        service_namespace: autoscaling
        target_tracking_configuration:
          predefined_scaling_metric_specification:
            predefined_scaling_metric_type: ASGAverageCPUUtilization
          target_value: 70
```

## Basic Predictive Scaling

```yaml
data:
  aws_availability_zones:
    available:

resource:
  aws_autoscaling_group:
    example:
      name_prefix: example
      launch_configuration: ${aws_launch_configuration.example.name}
      availability_zones: 
        - ${data.aws_availability_zones.available.names[0]}
      min_size: 0
      max_size: 3
      tags:
        - key: application

resource:
  aws_autoscalingplans_scaling_plan:
    example:
      name: example-predictive-cost-optimization
      application_source:
        tag_filter:
          key: application
          values: 
            - example
      scaling_instruction:
        disable_dynamic_scaling: true
        max_capacity: 3
        min_capacity: 0
        resource_id: example-formatted
        scalable_dimension: "autoscaling:autoScalingGroup:DesiredCapacity"
        service_namespace: autoscaling
        target_tracking_configuration:
          predefined_scaling_metric_specification:
            predefined_scaling_metric_type: ASGAverageCPUUtilization
          target_value: 70
        predictive_scaling_max_capacity_behavior: SetForecastCapacityToMaxCapacity
        predictive_scaling_mode: ForecastAndScale
        predefined_load_metric_specification:
          predefined_load_metric_type: ASGTotalCPUUtilization
```
