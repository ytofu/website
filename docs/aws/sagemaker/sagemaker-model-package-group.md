# Resource: aws_sagemaker_model_package_group

Provides a SageMaker AI Model Package Group resource.

## Basic Example

```yaml
resource:
  aws_sagemaker_model_package_group:
    example:
      model_package_group_name: example
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `model_package_group_name` - (Required) The name of the model group.
* `model_package_group_description` - (Optional) A description for the model group.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The name of the Model Package Group.
* `arn` - The Amazon Resource Name (ARN) assigned by AWS to this Model Package Group.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_sagemaker_model_package_group.test_model_package_group my-code-repo
```
