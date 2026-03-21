# Resource: aws_iam_role_policies_exclusive

ytofu resource for maintaining exclusive management of inline policies assigned to an AWS IAM (Identity & Access Management) role.

## Basic Example

```yaml
resource:
  aws_iam_role_policies_exclusive:
    example:
      role_name: ${aws_iam_role.example.name}
      policy_names: 
        - ${aws_iam_role_policy.example.name}
```

## Disallow Inline Policies

```yaml
resource:
  aws_iam_role_policies_exclusive:
    example:
      role_name: ${aws_iam_role.example.name}
      policy_names: []
```

## Argument Reference

The following arguments are required:

* `role_name` - (Required) IAM role name.
* `policy_names` - (Required) A list of inline policy names to be assigned to the role. Policies attached to this role but not configured in this argument will be removed.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_iam_role_policies_exclusive.example MyRole
```
