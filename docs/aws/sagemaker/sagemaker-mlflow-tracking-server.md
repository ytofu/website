# Sagemaker Mlflow Tracking Server

Manage Sagemaker Mlflow Tracking Server resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_mlflow_tracking_server:
    example:
      tracking_server_name: example
      role_arn: ${aws_iam_role.example.arn}
      artifact_store_uri: "s3://${aws_s3_bucket.example.bucket}/path"
```
