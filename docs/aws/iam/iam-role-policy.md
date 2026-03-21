# Resource: aws_iam_role_policy

Provides an IAM role inline policy.

## Basic Example

```yaml
resource:
  aws_iam_role_policy:
    test_policy:
      name: test_policy
      role: ${aws_iam_role.test_role.id}
      policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": [ "ec2:Describe*", ] "Effect": "Allow" "Resource": "*" }, ] }'

resource:
  aws_iam_role:
    test_role:
      name: test_role
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": "sts:AssumeRole" "Effect": "Allow" "Sid": "" "Principal": { "Service": "ec2.amazonaws.com" } }, ] }'
```

## Argument Reference

This resource supports the following arguments:

* `name` - (Optional) The name of the role policy.
  If omitted, ytofu will assign a random, unique name.
* `name_prefix` - (Optional) Creates a unique name beginning with the specified prefix.
  Conflicts with `name`.
* `policy` - (Required) The inline policy document.
  This is a JSON formatted string.
  For more information about building IAM policy documents with ytofu, see the [AWS IAM Policy Document Guide](https://learn.hashicorp.com/terraform/aws/iam-policy)
* `role` - (Required) The name of the IAM role to attach to the policy.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_iam_role_policy.example role_of_mypolicy_name:mypolicy_name
```
