# Resource: aws_sagemaker_mlflow_app

Provides a SageMaker AI MLflow App resource.

## Basic Example

```yaml
resource:
  aws_sagemaker_mlflow_app:
    example:
      name: example
      role_arn: ${aws_iam_role.example.arn}
      artifact_store_uri: "s3://${aws_s3_bucket.example.bucket}/path"
```

## Argument Reference

This resource supports the following arguments:

* `account_default_status` - (Optional) Indicates whether this MLflow app is the default for the entire account. Valid values are `ENABLED` and `DISABLED`.
* `artifact_store_uri` - (Required) S3 URI for a general purpose bucket to use as the MLflow App artifact store.
* `default_domain_id_list` - (Optional) List of SageMaker domain IDs for which this MLflow App is used as the default.
* `model_registration_mode` - (Optional) Whether to enable or disable automatic registration of new MLflow models to the SageMaker Model Registry. Valid values are `AutoModelRegistrationEnabled` and `AutoModelRegistrationDisabled`. Defaults to `AutoModelRegistrationDisabled`.
* `name` - (Required) MLflow app name.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `role_arn` - (Required) Amazon Resource Name (ARN) for an IAM role in your account that the MLflow App uses to access the artifact store in Amazon S3.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `weekly_maintenance_window_start` - (Optional) Day and time of the week in Coordinated Universal Time (UTC) 24-hour standard time that weekly maintenance updates are scheduled. For example: `SUN:03:00`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) of the MLflow App.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `create` - (Default `10m`)
* `update` - (Default `10m`)
* `delete` - (Default `10m`)

## Import

```bash
ytofu import aws_sagemaker_mlflow_app.example arn:aws:sagemaker:us-east-1:123456789012:mlflow-app/app-ABCD1234
```
