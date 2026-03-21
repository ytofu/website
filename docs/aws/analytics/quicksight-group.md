# Resource: aws_quicksight_group

Resource for managing QuickSight Group

## Basic Example

```yaml
resource:
  aws_quicksight_group:
    example:
      group_name: tf-example
```

## Argument Reference

This resource supports the following arguments:

* `aws_account_id` - (Optional, Forces new resource) AWS account ID. Defaults to automatically determined account ID of the ytofu AWS provider.
* `description` - (Optional) A description for the group.
* `group_name` - (Required) A name for the group.
* `namespace` - (Optional) The namespace. Currently, you should set this to `default`.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) of group

## Import

```bash
ytofu import aws_quicksight_group.example 123456789123/default/tf-example
```
