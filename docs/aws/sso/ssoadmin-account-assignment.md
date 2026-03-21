# Resource: aws_ssoadmin_account_assignment

Provides a Single Sign-On (SSO) Account Assignment resource

## Basic Example

```yaml
data:
  aws_ssoadmin_instances:
    example:

data:
  aws_ssoadmin_permission_set:
    example:
      instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}
      name: AWSReadOnlyAccess

data:
  aws_identitystore_group:
    example:
      identity_store_id: ${data.aws_ssoadmin_instances.example.identity_store_ids[0]}
      alternate_identifier:
        unique_attribute:
          attribute_path: DisplayName
          attribute_value: ExampleGroup

resource:
  aws_ssoadmin_account_assignment:
    example:
      instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}
      permission_set_arn: ${data.aws_ssoadmin_permission_set.example.arn}
      principal_id: ${data.aws_identitystore_group.example.group_id}
      principal_type: GROUP
      target_id: 123456789012
      target_type: AWS_ACCOUNT
```

## With Managed Policy Attachment

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

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `instance_arn` - (Required, Forces new resource) The Amazon Resource Name (ARN) of the SSO Instance.
* `permission_set_arn` - (Required, Forces new resource) The Amazon Resource Name (ARN) of the Permission Set that the admin wants to grant the principal access to.
* `principal_id` - (Required, Forces new resource) An identifier for an object in SSO, such as a user or group. PrincipalIds are GUIDs (For example, `f81d4fae-7dec-11d0-a765-00a0c91e6bf6`).
* `principal_type` - (Required, Forces new resource) The entity type for which the assignment will be created. Valid values: `USER`, `GROUP`.
* `target_id` - (Required, Forces new resource) An AWS account identifier, typically a 10-12 digit string.
* `target_type` - (Required, Forces new resource) The entity type for which the assignment will be created. Valid values: `AWS_ACCOUNT`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The identifier of the Account Assignment i.e., `principal_id`, `principal_type`, `target_id`, `target_type`, `permission_set_arn`, `instance_arn` separated by commas (`,`).

## Timeouts

Configuration options:

- `create` - (Default `5m`)
- `delete` - (Default `5m`)

## Import

```bash
ytofu import aws_ssoadmin_account_assignment.example f81d4fae-7dec-11d0-a765-00a0c91e6bf6,GROUP,1234567890,AWS_ACCOUNT,arn:aws:sso:::permissionSet/ssoins-0123456789abcdef/ps-0123456789abcdef,arn:aws:sso:::instance/ssoins-0123456789abcdef
```
