# Evidently Launch

Manage Evidently Launch resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_evidently_launch:
    example:
      name: example
      project: ${aws_evidently_project.example.name}
      groups:
        feature: ${aws_evidently_feature.example.name}
        name: Variation1
        variation: Variation1
      scheduled_splits_config:
        steps:
          group_weights: 
          start_time: "2024-01-07 01:43:59+00:00"
```

## With description

```yaml
resource:
  aws_evidently_launch:
    example:
      name: example
      project: ${aws_evidently_project.example.name}
      description: example description
      groups:
        feature: ${aws_evidently_feature.example.name}
        name: Variation1
        variation: Variation1
      scheduled_splits_config:
        steps:
          group_weights: 
          start_time: "2024-01-07 01:43:59+00:00"
```

## With multiple groups

```yaml
resource:
  aws_evidently_launch:
    example:
      name: example
      project: ${aws_evidently_project.example.name}
      groups:
        feature: ${aws_evidently_feature.example.name}
        name: Variation1
        variation: Variation1
        description: first-group
      groups:
        feature: ${aws_evidently_feature.example.name}
        name: Variation2
        variation: Variation2
        description: second-group
      scheduled_splits_config:
        steps:
          group_weights: 
          start_time: "2024-01-07 01:43:59+00:00"
```

## With metric_monitors

```yaml
resource:
  aws_evidently_launch:
    example:
      name: example
      project: ${aws_evidently_project.example.name}
      groups:
        feature: ${aws_evidently_feature.example.name}
        name: Variation1
        variation: Variation1
      metric_monitors:
        metric_definition:
          entity_id_key: entity_id_key1
          event_pattern: "{\"Price\":[{\"numeric\":[\">\",11,\"<=\",22]}]}"
          name: name1
          unit_label: unit_label1
          value_key: value_key1
      metric_monitors:
        metric_definition:
          entity_id_key: entity_id_key2
          event_pattern: "{\"Price\":[{\"numeric\":[\">\",9,\"<=\",19]}]}"
          name: name2
          unit_label: unit_label2
          value_key: value_key2
      scheduled_splits_config:
        steps:
          group_weights: 
          start_time: "2024-01-07 01:43:59+00:00"
```

## With randomization_salt

```yaml
resource:
  aws_evidently_launch:
    example:
      name: example
      project: ${aws_evidently_project.example.name}
      randomization_salt: example randomization salt
      groups:
        feature: ${aws_evidently_feature.example.name}
        name: Variation1
        variation: Variation1
      scheduled_splits_config:
        steps:
          group_weights: 
          start_time: "2024-01-07 01:43:59+00:00"
```

## With multiple steps

```yaml
resource:
  aws_evidently_launch:
    example:
      name: example
      project: ${aws_evidently_project.example.name}
      groups:
        feature: ${aws_evidently_feature.example.name}
        name: Variation1
        variation: Variation1
      groups:
        feature: ${aws_evidently_feature.example.name}
        name: Variation2
        variation: Variation2
      scheduled_splits_config:
        steps:
          group_weights: 
          start_time: "2024-01-07 01:43:59+00:00"
        steps:
          group_weights: 
          start_time: "2024-01-08 01:43:59+00:00"
```

## With segment overrides

```yaml
resource:
  aws_evidently_launch:
    example:
      name: example
      project: ${aws_evidently_project.example.name}
      groups:
        feature: ${aws_evidently_feature.example.name}
        name: Variation1
        variation: Variation1
      groups:
        feature: ${aws_evidently_feature.example.name}
        name: Variation2
        variation: Variation2
      scheduled_splits_config:
        steps:
          group_weights: 
          segment_overrides:
            evaluation_order: 1
            segment: ${aws_evidently_segment.example.name}
            weights: 
          segment_overrides:
            evaluation_order: 2
            segment: ${aws_evidently_segment.example.name}
            weights: 
          start_time: "2024-01-08 01:43:59+00:00"
```
