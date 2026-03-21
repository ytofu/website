# Resource: aws_iam_user_policies_exclusive

ytofu resource for maintaining exclusive management of inline policies assigned to an AWS IAM (Identity & Access Management) user.

## Basic Example

```yaml
resource:
  aws_iam_user_policies_exclusive:
    example:
      user_name: ${aws_iam_user.example.name}
      policy_names: 
        - ${aws_iam_user_policy.example.name}
```

## Disallow Inline Policies

```yaml
resource:
  aws_iam_user_policies_exclusive:
    example:
      user_name: ${aws_iam_user.example.name}
      policy_names: []
```

## Argument Reference

The following arguments are required:

* `user_name` - (Required) IAM user name.
* `policy_names` - (Required) A list of inline policy names to be assigned to the user. Policies attached to this user but not configured in this argument will be removed.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_iam_user_policies_exclusive.example MyUser
```
