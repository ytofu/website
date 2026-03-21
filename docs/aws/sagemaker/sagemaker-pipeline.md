# Sagemaker Pipeline

Manage Sagemaker Pipeline resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_pipeline:
    example:
      pipeline_name: example
      pipeline_display_name: example
      role_arn: ${aws_iam_role.example.arn}
      pipeline_definition: '{ "Version": "2020-12-01" "Steps": [{ "Name": "Test" "Type": "Fail" "Arguments": { "ErrorMessage": "test" } }] }'
```
