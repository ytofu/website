# Resource: aws_quicksight_role_membership

ytofu resource for managing an AWS QuickSight Role Membership.

## Basic Example

```yaml
resource:
  aws_quicksight_role_membership:
    example:
      member_name: example-group
      role: READER
```

## Argument Reference

The following arguments are required:

* `member_name` - (Required) Name of the group to be added to the role.
* `role` - (Required) Role to add the group to. Valid values are `ADMIN`, `AUTHOR`, `READER`, `ADMIN_PRO`, `AUTHOR_PRO`, and `READER_PRO`.

The following arguments are optional:

* `aws_account_id` - (Optional, Forces new resource) AWS account ID. Defaults to automatically determined account ID of the ytofu AWS provider.
* `namespace` - (Optional) Name of the namespace. Defaults to `default`.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_quicksight_role_membership.example 012345678901,default,READER,example-group
```
