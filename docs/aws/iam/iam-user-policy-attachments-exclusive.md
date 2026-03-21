# IAM User Policy Attachments Exclusive

Manage IAM User Policy Attachments Exclusive resources using ytofu YAML.

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
