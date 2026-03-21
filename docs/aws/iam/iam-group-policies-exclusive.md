# IAM Group Policies Exclusive

Manage IAM Group Policies Exclusive resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iam_group_policies_exclusive:
    example:
      group_name: ${aws_iam_group.example.name}
      policy_names: 
        - ${aws_iam_group_policy.example.name}
```

## Disallow Inline Policies

```yaml
resource:
  aws_iam_group_policies_exclusive:
    example:
      group_name: ${aws_iam_group.example.name}
      policy_names: []
```
