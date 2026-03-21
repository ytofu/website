# Resource: aws_quicksight_template_alias

ytofu resource for managing an AWS QuickSight Template Alias.

## Basic Example

```yaml
resource:
  aws_quicksight_template_alias:
    example:
      alias_name: example-alias
      template_id: ${aws_quicksight_template.test.template_id}
      template_version_number: ${aws_quicksight_template.test.version_number}
```

## Argument Reference

The following arguments are required:

* `alias_name` - (Required, Forces new resource) Display name of the template alias.
* `template_id` - (Required, Forces new resource) ID of the template.
* `template_version_number` - (Required) Version number of the template.

The following arguments are optional:

* `aws_account_id` - (Optional, Forces new resource) AWS account ID. Defaults to automatically determined account ID of the ytofu AWS provider.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) of the template alias.
* `id` - A comma-delimited string joining AWS account ID, template ID, and alias name.

## Import

```bash
ytofu import aws_quicksight_template_alias.example 123456789012,example-id,example-alias
```
