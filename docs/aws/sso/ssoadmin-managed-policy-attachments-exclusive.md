# Resource: aws_ssoadmin_managed_policy_attachments_exclusive

ytofu resource for managing exclusive AWS SSO Admin Managed Policy Attachments.

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

## Argument Reference

The following arguments are required:

* `instance_arn` - (Required) ARN of the SSO Instance.
* `managed_policy_arns` - (Required) Set of ARNs of IAM managed policies to attach to the Permission Set.
* `permission_set_arn` - (Required) ARN of the Permission Set.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports no additional attributes.

## Timeouts

Configuration options:

* `create` - (Default `10m`)
* `update` - (Default `10m`)

## Import

```bash
ytofu import aws_ssoadmin_managed_policy_attachments_exclusive.example arn:aws:sso:::instance/ssoins-1234567890abcdef,arn:aws:sso:::permissionSet/ssoins-1234567890abcdef/ps-1234567890abcdef
```
