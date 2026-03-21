# Resource: aws_quicksight_group_membership

Resource for managing QuickSight Group Membership

## Basic Example

```yaml
resource:
  aws_quicksight_group_membership:
    example:
      group_name: all-access-users
      member_name: john_smith
```

## Argument Reference

This resource supports the following arguments:

* `aws_account_id` - (Optional, Forces new resource) AWS account ID. Defaults to automatically determined account ID of the ytofu AWS provider.
* `group_name` - (Required) The name of the group in which the member will be added.
* `member_name` - (Required) The name of the member to add to the group.
* `namespace` - (Optional) The namespace that you want the user to be a part of. Defaults to `default`.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_quicksight_group_membership.example 123456789123/default/all-access-users/john_smith
```
