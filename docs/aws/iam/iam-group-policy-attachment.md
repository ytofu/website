# IAM Group Policy Attachment

Manage IAM Group Policy Attachment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iam_group:
    group:
      name: test-group

resource:
  aws_iam_policy:
    policy:
      name: test-policy
      description: A test policy
      policy: "{ ... policy JSON ... }"

resource:
  aws_iam_group_policy_attachment:
    test-attach:
      group: ${aws_iam_group.group.name}
      policy_arn: ${aws_iam_policy.policy.arn}
```
