# Resource: aws_iam_group_policy_attachments_exclusive

ytofu resource for maintaining exclusive management of managed IAM policies assigned to an AWS IAM (Identity & Access Management) group.

## Basic Example

```yaml
resource:
  aws_iam_group_policy_attachments_exclusive:
    example:
      group_name: ${aws_iam_group.example.name}
      policy_arns: 
        - ${aws_iam_policy.example.arn}
```

## Disallow Managed IAM Policies

```yaml
resource:
  aws_iam_group_policy_attachments_exclusive:
    example:
      group_name: ${aws_iam_group.example.name}
      policy_arns: []
```

## Argument Reference

The following arguments are required:

* `group_name` - (Required) IAM group name.
* `policy_arns` - (Required) A list of managed IAM policy ARNs to be attached to the group. Policies attached to this group but not configured in this argument will be removed.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_iam_group_policy_attachments_exclusive.example MyGroup
```
