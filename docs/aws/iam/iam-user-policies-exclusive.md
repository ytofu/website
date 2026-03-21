# IAM User Policies Exclusive

Manage IAM User Policies Exclusive resources using ytofu YAML.

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
