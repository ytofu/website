# Resource: aws_iam_group_policies_exclusive

ytofu resource for maintaining exclusive management of inline policies assigned to an AWS IAM (Identity & Access Management) group.

## Basic Example

```yaml
resource:
  aws_iam_group_policies_exclusive:
    example:
      group_name: ${aws_iam_group.example.name}
      policy_names: 
        - ${aws_iam_group_policy.example.name}
```

## Disallow Inline Policies

```yaml
resource:
  aws_iam_group_policies_exclusive:
    example:
      group_name: ${aws_iam_group.example.name}
      policy_names: []
```

## Argument Reference

The following arguments are required:

* `group_name` - (Required) IAM group name.
* `policy_names` - (Required) A list of inline policy names to be assigned to the group. Policies attached to this group but not configured in this argument will be removed.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_iam_group_policies_exclusive.example MyGroup
```
