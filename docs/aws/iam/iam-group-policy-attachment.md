# Resource: aws_iam_group_policy_attachment

Attaches a Managed IAM Policy to an IAM group

## Basic Example

```yaml
resource:
  aws_iam_group:
    group:
      name: test-group

  aws_iam_policy:
    policy:
      name: test-policy
      description: A test policy
      policy: "{ ... policy JSON ... }"

  aws_iam_group_policy_attachment:
    test-attach:
      group: ${aws_iam_group.group.name}
      policy_arn: ${aws_iam_policy.policy.arn}```

## Argument Reference

This resource supports the following arguments:

* `group`  (Required) - The group the policy should be applied to
* `policy_arn`  (Required) - The ARN of the policy you want to apply

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_iam_group_policy_attachment.test-attach test-group/arn:aws:iam::xxxxxxxxxxxx:policy/test-policy
```
