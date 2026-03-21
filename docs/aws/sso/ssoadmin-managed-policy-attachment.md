# Ssoadmin Managed Policy Attachment

Manage Ssoadmin Managed Policy Attachment resources using ytofu YAML.

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
  aws_ssoadmin_managed_policy_attachment:
    example:
      instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}
      managed_policy_arn: "arn:aws:iam::aws:policy/AlexaForBusinessDeviceSetup"
      permission_set_arn: ${aws_ssoadmin_permission_set.example.arn}
```

## With Account Assignment

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
  aws_identitystore_group:
    example:
      identity_store_id: ${data.aws_ssoadmin_instances.example.identity_store_ids[0]}
      display_name: Admin
      description: Admin Group

resource:
  aws_ssoadmin_account_assignment:
    example:
      instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}
      permission_set_arn: ${aws_ssoadmin_permission_set.example.arn}
      principal_id: ${aws_identitystore_group.example.group_id}
      principal_type: GROUP
      target_id: 123456789012
      target_type: AWS_ACCOUNT

resource:
  aws_ssoadmin_managed_policy_attachment:
    example:
      depends_on: 
        - ${aws_ssoadmin_account_assignment.example}
      instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}
      managed_policy_arn: "arn:aws:iam::aws:policy/AlexaForBusinessDeviceSetup"
      permission_set_arn: ${aws_ssoadmin_permission_set.example.arn}
```
