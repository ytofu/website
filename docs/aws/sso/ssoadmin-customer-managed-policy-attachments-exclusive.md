# Resource: aws_ssoadmin_customer_managed_policy_attachments_exclusive

ytofu resource for managing exclusive AWS SSO Admin Customer Managed Policy Attachments.

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

  aws_iam_policy:
    example:
      name: TestPolicy
      description: My test policy
      policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": [ "ec2:Describe*", ] "Effect": "Allow" "Resource": "*" }, ] }'

  aws_ssoadmin_customer_managed_policy_attachments_exclusive:
    example:
      instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}
      permission_set_arn: ${aws_ssoadmin_permission_set.example.arn}
      customer_managed_policy_reference:
        name: ${aws_iam_policy.example.name}
        path: /```

## Disallow Customer Managed Policy Attachments

```yaml
resource:
  aws_ssoadmin_customer_managed_policy_attachments_exclusive:
    example:
      instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}
      permission_set_arn: ${aws_ssoadmin_permission_set.example.arn}
```

## Argument Reference

The following arguments are required:

* `instance_arn` - (Required) ARN of the SSO Instance.
* `permission_set_arn` - (Required) ARN of the Permission Set.

The following arguments are optional:

* `customer_managed_policy_reference` - (Optional) Specifies the names and paths of the customer managed policies to attach. See [Customer Managed Policy Reference](#customer-managed-policy-reference) below.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

### Customer Managed Policy Reference

The `customer_managed_policy_reference` block describes a customer managed IAM policy. You must have an IAM policy that matches the name and path in each AWS account where you want to deploy your specified permission set.

* `name` - (Required) Name of the customer managed IAM Policy to be attached.
* `path` - (Optional) The path to the IAM policy to be attached. The default is `/`. See [IAM Identifiers](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_identifiers.html#identifiers-friendly-names) for more information.

## Attribute Reference

This resource exports no additional attributes.

## Timeouts

Configuration options:

* `create` - (Default `10m`)
* `update` - (Default `10m`)

## Import

```bash
ytofu import aws_ssoadmin_customer_managed_policy_attachments_exclusive.example arn:aws:sso:::instance/ssoins-1234567890abcdef,arn:aws:sso:::permissionSet/ssoins-1234567890abcdef/ps-1234567890abcdef
```
