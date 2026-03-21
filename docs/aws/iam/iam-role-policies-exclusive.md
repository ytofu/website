# IAM Role Policies Exclusive

Manage IAM Role Policies Exclusive resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iam_role_policies_exclusive:
    example:
      role_name: ${aws_iam_role.example.name}
      policy_names: 
        - ${aws_iam_role_policy.example.name}
```

## Disallow Inline Policies

```yaml
resource:
  aws_iam_role_policies_exclusive:
    example:
      role_name: ${aws_iam_role.example.name}
      policy_names: []
```
