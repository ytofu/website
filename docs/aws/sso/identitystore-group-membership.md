# Resource: aws_identitystore_group_membership

ytofu resource for managing an AWS IdentityStore Group Membership.

## Basic Example

```yaml
data:
  aws_ssoadmin_instances:
    example:

resource:
  aws_identitystore_user:
    example:
      identity_store_id: ${data.aws_ssoadmin_instances.example.identity_store_ids[0]}
      display_name: John Doe
      user_name: john.doe@example.com
      name:
        family_name: Doe
        given_name: John

resource:
  aws_identitystore_group:
    example:
      identity_store_id: ${data.aws_ssoadmin_instances.example.identity_store_ids[0]}
      display_name: MyGroup
      description: Some group name

resource:
  aws_identitystore_group_membership:
    example:
      identity_store_id: ${data.aws_ssoadmin_instances.example.identity_store_ids[0]}
      group_id: ${aws_identitystore_group.example.group_id}
      member_id: ${aws_identitystore_user.example.user_id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `member_id` - (Required) The identifier for a user in the Identity Store.
* `group_id` - (Required)  The identifier for a group in the Identity Store.
* `identity_store_id` - (Required) Identity Store ID associated with the Single Sign-On Instance.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `membership_id` - The identifier of the newly created group membership in the Identity Store.

## Import

```bash
ytofu import aws_identitystore_group_membership.example d-0000000000/00000000-0000-0000-0000-000000000000
```
