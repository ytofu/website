# IAM Group Policy Attachments Exclusive

Manage IAM Group Policy Attachments Exclusive resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iam_group_policy_attachments_exclusive:
    example:
      group_name: ${aws_iam_group.example.name}
      policy_arns: 
        - ${aws_iam_policy.example.arn}
```

## Disallow Managed IAM Policies

```yaml
resource:
  aws_iam_group_policy_attachments_exclusive:
    example:
      group_name: ${aws_iam_group.example.name}
      policy_arns: []
```
