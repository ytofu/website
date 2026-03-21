# Resource: aws_sagemaker_notebook_instance_lifecycle_configuration

Provides a lifecycle configuration for SageMaker AI Notebook Instances.

## Basic Example

```yaml
resource:
  aws_sagemaker_notebook_instance_lifecycle_configuration:
    lc:
      name: foo
      on_create: base64-encoded-content
      on_start: base64-encoded-content
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Optional) The name of the lifecycle configuration (must be unique). If omitted, ytofu will assign a random, unique name.
* `on_create` - (Optional) A shell script (base64-encoded) that runs only once when the SageMaker AI Notebook Instance is created.
* `on_start` - (Optional) A shell script (base64-encoded) that runs every time the SageMaker AI Notebook Instance is started including the time it's created.
* `tags` - (Optional) A mapping of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The Amazon Resource Name (ARN) assigned by AWS to this lifecycle configuration.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_sagemaker_notebook_instance_lifecycle_configuration.lc foo
```
