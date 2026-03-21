# Ssoadmin Customer Managed Policy Attachments Exclusive

Manage Ssoadmin Customer Managed Policy Attachments Exclusive resources using ytofu YAML.

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
  aws_iam_policy:
    example:
      name: TestPolicy
      description: My test policy
      policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": [ "ec2:Describe*", ] "Effect": "Allow" "Resource": "*" }, ] }'

resource:
  aws_ssoadmin_customer_managed_policy_attachments_exclusive:
    example:
      instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}
      permission_set_arn: ${aws_ssoadmin_permission_set.example.arn}
      customer_managed_policy_reference:
        name: ${aws_iam_policy.example.name}
        path: /
```

## Disallow Customer Managed Policy Attachments

```yaml
resource:
  aws_ssoadmin_customer_managed_policy_attachments_exclusive:
    example:
      instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}
      permission_set_arn: ${aws_ssoadmin_permission_set.example.arn}
```
