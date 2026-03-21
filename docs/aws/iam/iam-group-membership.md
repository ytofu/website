# Resource: aws_iam_group_membership



## Basic Example

```yaml
resource:
  aws_iam_group_membership:
    team:
      name: tf-testing-group-membership
      users:
        - ${aws_iam_user.user_one.name}
        - ${aws_iam_user.user_two.name}
      group: ${aws_iam_group.group.name}

  aws_iam_group:
    group:
      name: test-group

  aws_iam_user:
    user_one:
      name: test-user

  aws_iam_user:
    user_two:
      name: test-user-two```

## Argument Reference

This resource supports the following arguments:

* `name` - (Required) The name to identify the Group Membership
* `users` - (Required) A list of IAM User names to associate with the Group
* `group` - (Required) The IAM Group name to attach the list of `users` to

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `name` - The name to identify the Group Membership
* `users` - list of IAM User names
* `group` - IAM Group name

[1]: /docs/providers/aws/r/iam_group.html
[2]: /docs/providers/aws/r/iam_user.html
[3]: /docs/providers/aws/r/iam_user_group_membership.html
