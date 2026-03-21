# IAM User Policy Attachment

Manage IAM User Policy Attachment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iam_user:
    user:
      name: test-user

resource:
  aws_iam_policy:
    policy:
      name: test-policy
      description: A test policy
      policy: "{ ... policy JSON ... }"

resource:
  aws_iam_user_policy_attachment:
    test-attach:
      user: ${aws_iam_user.user.name}
      policy_arn: ${aws_iam_policy.policy.arn}
```
