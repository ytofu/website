# SSO Managed Policy Attachment

Attach managed policies to permission sets using ytofu YAML.

## AWS Managed Policy

```yaml
resource:
  aws_ssoadmin_managed_policy_attachment:
    example:
      instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}
      managed_policy_arn: arn:aws:iam::aws:policy/AdministratorAccess
      permission_set_arn: ${aws_ssoadmin_permission_set.example.arn}
```

## Customer Managed Policy

```yaml
resource:
  aws_ssoadmin_customer_managed_policy_attachment:
    example:
      instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}
      permission_set_arn: ${aws_ssoadmin_permission_set.example.arn}
      customer_managed_policy_reference:
        name: CustomPolicy
        path: /
```
