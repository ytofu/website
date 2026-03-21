# Resource: aws_iam_user_policy_attachment

Attaches a Managed IAM Policy to an IAM user

## Basic Example

```yaml
resource:
  aws_iam_user:
    user:
      name: test-user

  aws_iam_policy:
    policy:
      name: test-policy
      description: A test policy
      policy: "{ ... policy JSON ... }"

  aws_iam_user_policy_attachment:
    test-attach:
      user: ${aws_iam_user.user.name}
      policy_arn: ${aws_iam_policy.policy.arn}```

## Argument Reference

This resource supports the following arguments:

* `user`        (Required) - The user the policy should be applied to
* `policy_arn`  (Required) - The ARN of the policy you want to apply

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_iam_user_policy_attachment.test-attach test-user/arn:aws:iam::xxxxxxxxxxxx:policy/test-policy
```
