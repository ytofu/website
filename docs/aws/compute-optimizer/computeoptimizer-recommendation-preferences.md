# Computeoptimizer Recommendation Preferences

Manage Computeoptimizer Recommendation Preferences resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_computeoptimizer_recommendation_preferences:
    example:
      resource_type: Ec2Instance
      scope:
        name: AccountId
        value: 123456789012
      look_back_period: DAYS_32
```

## Multiple Preferences

```yaml
resource:
  aws_computeoptimizer_recommendation_preferences:
    example:
      resource_type: Ec2Instance
      scope:
        name: AccountId
        value: 123456789012
      enhanced_infrastructure_metrics: Active
      external_metrics_preference:
        source: Datadog
      preferred_resource:
        include_list: 
          - m5.xlarge
          - r5
        name: Ec2InstanceTypes
```
