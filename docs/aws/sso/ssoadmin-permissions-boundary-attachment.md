# Ssoadmin Permissions Boundary Attachment

Manage Ssoadmin Permissions Boundary Attachment resources using ytofu YAML.

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
  aws_ssoadmin_permissions_boundary_attachment:
    example:
      instance_arn: ${aws_ssoadmin_permission_set.example.instance_arn}
      permission_set_arn: ${aws_ssoadmin_permission_set.example.arn}
      permissions_boundary:
        customer_managed_policy_reference:
          name: ${aws_iam_policy.example.name}
          path: /
```

## Attaching an AWS-managed policy

```yaml
resource:
  aws_ssoadmin_permissions_boundary_attachment:
    example:
      instance_arn: ${aws_ssoadmin_permission_set.example.instance_arn}
      permission_set_arn: ${aws_ssoadmin_permission_set.example.arn}
      permissions_boundary:
        managed_policy_arn: "arn:aws:iam::aws:policy/ReadOnlyAccess"
```
