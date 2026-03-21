# Sagemaker Monitoring Schedule

Manage Sagemaker Monitoring Schedule resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_monitoring_schedule:
    test:
      name: my-monitoring-schedule
      monitoring_schedule_config:
        monitoring_job_definition_name: ${aws_sagemaker_data_quality_job_definition.test.name}
        monitoring_type: DataQuality
```
