# Resource: aws_quicksight_user_custom_permission

Manages the custom permissions profile for a user.

## Basic Example

```yaml
resource:
  aws_quicksight_user_custom_permission:
    example:
      user_name: ${aws_quicksight_user.example.user_name}
      custom_permissions_name: ${aws_quicksight_custom_permissions.example.custom_permissions_name}
```

## Argument Reference

The following arguments are required:

* `custom_permissions_name` - (Required, Forces new resource) Custom permissions profile name.
* `user_name` - (Required, Forces new resource) Username of the user.

The following arguments are optional:

* `aws_account_id` - (Optional, Forces new resource) AWS account ID. Defaults to automatically determined account ID of the ytofu AWS provider.
* `namespace` - (Optional, Forces new resource) Namespace that the user belongs to. Defaults to `default`.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_quicksight_user_custom_permission.example 012345678901,default,user1
```
