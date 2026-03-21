# IAM Role Policy Attachments Exclusive

Manage IAM Role Policy Attachments Exclusive resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iam_role_policy_attachments_exclusive:
    example:
      role_name: ${aws_iam_role.example.name}
      policy_arns: 
        - ${aws_iam_policy.example.arn}
```

## Disallow Managed IAM Policies

```yaml
resource:
  aws_iam_role_policy_attachments_exclusive:
    example:
      role_name: ${aws_iam_role.example.name}
      policy_arns: []
```
