# Emrcontainers Job Template

Manage Emrcontainers Job Template resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_emrcontainers_job_template:
    example:
      job_template_data:
        execution_role_arn: ${aws_iam_role.example.arn}
        release_label: emr-6.10.0-latest
        job_driver:
          spark_sql_job_driver:
            entry_point: default
      name: example
```
