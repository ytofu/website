# Resource: aws_ssoadmin_managed_policy_attachment

Provides an IAM managed policy for a Single Sign-On (SSO) Permission Set resource

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

## Argument Reference

This resource supports the following arguments:

* `instance_arn` - (Required, Forces new resource) The Amazon Resource Name (ARN) of the SSO Instance under which the operation will be executed.
* `managed_policy_arn` - (Required, Forces new resource) The IAM managed policy Amazon Resource Name (ARN) to be attached to the Permission Set.
* `permission_set_arn` - (Required, Forces new resource) The Amazon Resource Name (ARN) of the Permission Set.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The Amazon Resource Names (ARNs) of the Managed Policy, Permission Set, and SSO Instance, separated by a comma (`,`).
* `managed_policy_name` - The name of the IAM Managed Policy.

## Timeouts

Configuration options:

- `create` - (Default `10m`)
- `delete` - (Default `10m`)

## Import

```bash
ytofu import aws_ssoadmin_managed_policy_attachment.example arn:aws:iam::aws:policy/AlexaForBusinessDeviceSetup,arn:aws:sso:::permissionSet/ssoins-2938j0x8920sbj72/ps-80383020jr9302rk,arn:aws:sso:::instance/ssoins-2938j0x8920sbj72
```
