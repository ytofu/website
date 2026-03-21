# Ssoadmin Managed Policy Attachments Exclusive

Manage Ssoadmin Managed Policy Attachments Exclusive resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_ssoadmin_instances:
    example:

resource:
  aws_ssoadmin_permission_set:
    example:
      name: Example
      instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}

resource:
  aws_ssoadmin_managed_policy_attachments_exclusive:
    example:
      instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}
      permission_set_arn: ${aws_ssoadmin_permission_set.example.arn}
      managed_policy_arns:
        - "arn:aws:iam::aws:policy/ReadOnlyAccess"
```

## Disallow Managed Policy Attachments

```yaml
resource:
  aws_ssoadmin_managed_policy_attachments_exclusive:
    example:
      instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}
      permission_set_arn: ${aws_ssoadmin_permission_set.example.arn}
      managed_policy_arns: []
```
