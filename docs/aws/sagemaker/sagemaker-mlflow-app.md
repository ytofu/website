# Sagemaker Mlflow App

Manage Sagemaker Mlflow App resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_mlflow_app:
    example:
      name: example
      role_arn: ${aws_iam_role.example.arn}
      artifact_store_uri: "s3://${aws_s3_bucket.example.bucket}/path"
```
