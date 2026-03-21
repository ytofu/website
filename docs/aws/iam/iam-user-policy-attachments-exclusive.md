# Resource: aws_iam_user_policy_attachments_exclusive

ytofu resource for maintaining exclusive management of managed IAM policies assigned to an AWS IAM (Identity & Access Management) user.

## Basic Example

```yaml
resource:
  aws_iam_user_policy_attachments_exclusive:
    example:
      user_name: ${aws_iam_user.example.name}
      policy_arns: 
        - ${aws_iam_policy.example.arn}
```

## Disallow Managed IAM Policies

```yaml
resource:
  aws_iam_user_policy_attachments_exclusive:
    example:
      user_name: ${aws_iam_user.example.name}
      policy_arns: []
```

## Argument Reference

The following arguments are required:

* `user_name` - (Required) IAM user name.
* `policy_arns` - (Required) A list of managed IAM policy ARNs to be attached to the user. Policies attached to this user but not configured in this argument will be removed.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_iam_user_policy_attachments_exclusive.example MyUser
```
