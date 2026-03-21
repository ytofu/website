# Codebuild Fleet

Manage Codebuild Fleet resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_codebuild_fleet:
    test:
      base_capacity: 2
      compute_type: BUILD_GENERAL1_SMALL
      environment_type: LINUX_CONTAINER
      name: full-example-codebuild-fleet
      overflow_behavior: QUEUE
      scaling_configuration:
        max_capacity: 5
        scaling_type: TARGET_TRACKING_SCALING
        target_tracking_scaling_configs:
          metric_type: FLEET_UTILIZATION_RATE
          target_value: 97.5
```

## Basic Usage

```yaml
resource:
  aws_codebuild_fleet:
    example:
      name: example-codebuild-fleet
```
