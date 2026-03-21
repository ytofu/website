# Resource: aws_iam_role_policy_attachments_exclusive

ytofu resource for maintaining exclusive management of managed IAM policies assigned to an AWS IAM (Identity & Access Management) role.

## Basic Example

```yaml
resource:
  aws_iam_role_policy_attachments_exclusive:
    example:
      role_name: ${aws_iam_role.example.name}
      policy_arns: 
        - ${aws_iam_policy.example.arn}
```

## Disallow Managed IAM Policies

```yaml
resource:
  aws_iam_role_policy_attachments_exclusive:
    example:
      role_name: ${aws_iam_role.example.name}
      policy_arns: []
```

## Argument Reference

The following arguments are required:

* `role_name` - (Required) IAM role name.
* `policy_arns` - (Required) A list of managed IAM policy ARNs to be attached to the role. Policies attached to this role but not configured in this argument will be removed.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_iam_role_policy_attachments_exclusive.example MyRole
```
