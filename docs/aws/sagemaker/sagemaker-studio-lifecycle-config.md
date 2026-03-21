# Resource: aws_sagemaker_studio_lifecycle_config

Provides a SageMaker AI Studio Lifecycle Config resource.

## Basic Example

```yaml
resource:
  aws_sagemaker_studio_lifecycle_config:
    example:
      studio_lifecycle_config_name: example
      studio_lifecycle_config_app_type: JupyterServer
      studio_lifecycle_config_content: base64-encoded-content
```

## Argument Reference

This resource supports the following arguments:

- `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
- `studio_lifecycle_config_name` - (Required) The name of the Studio Lifecycle Configuration to create.
- `studio_lifecycle_config_app_type` - (Required) The App type that the Lifecycle Configuration is attached to. Valid values are `JupyterServer`, `JupyterLab`, `CodeEditor` and `KernelGateway`.
- `studio_lifecycle_config_content` - (Required) The content of your Studio Lifecycle Configuration script. This content must be base64 encoded.
- `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

- `id` - The name of the Studio Lifecycle Config.
- `arn` - The Amazon Resource Name (ARN) assigned by AWS to this Studio Lifecycle Config.
- `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_sagemaker_studio_lifecycle_config.example example
```
