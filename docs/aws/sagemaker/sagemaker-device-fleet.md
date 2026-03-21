# Sagemaker Device Fleet

Manage Sagemaker Device Fleet resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_device_fleet:
    example:
      device_fleet_name: example
      role_arn: ${aws_iam_role.test.arn}
      output_config:
        s3_output_location: "s3://${aws_s3_bucket.example.bucket}/prefix/"
```
