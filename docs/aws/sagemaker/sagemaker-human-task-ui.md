# Resource: aws_sagemaker_human_task_ui

Provides a SageMaker AI Human Task UI resource.

## Basic Example

```yaml
resource:
  aws_sagemaker_human_task_ui:
    example:
      human_task_ui_name: example
      ui_template:
        content: file-content
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `human_task_ui_name` - (Required) The name of the Human Task UI.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `ui_template` - (Required) The Liquid template for the worker user interface. See [UI Template](#ui-template) below.

### UI Template

* `content` - (Required) The content of the Liquid template for the worker user interface.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The Amazon Resource Name (ARN) assigned by AWS to this Human Task UI.
* `id` - The name of the Human Task UI.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
* `ui_template` - (Required) The Liquid template for the worker user interface. See [UI Template](#ui-template) below.

### UI Template

* `content_sha256` - The SHA-256 digest of the contents of the template.
* `url` - The URL for the user interface template.

## Import

```bash
ytofu import aws_sagemaker_human_task_ui.example example
```
