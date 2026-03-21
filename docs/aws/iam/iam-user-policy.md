# Resource: aws_iam_user_policy

Provides an IAM policy attached to a user.

## Basic Example

```yaml
resource:
  aws_iam_user_policy:
    lb_ro:
      name: test
      user: ${aws_iam_user.lb.name}
      policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": [ "ec2:Describe*", ] "Effect": "Allow" "Resource": "*" }, ] }'

  aws_iam_user:
    lb:
      name: loadbalancer
      path: /system/

  aws_iam_access_key:
    lb:
      user: ${aws_iam_user.lb.name}```

## Argument Reference

This resource supports the following arguments:

* `policy` - (Required) The policy document. This is a JSON formatted string. For more information about building AWS IAM policy documents with ytofu, see the [AWS IAM Policy Document Guide](https://learn.hashicorp.com/terraform/aws/iam-policy).
* `name` - (Optional) The name of the policy. If omitted, ytofu will assign a random, unique name.
* `name_prefix` - (Optional, Forces new resource) Creates a unique name beginning with the specified prefix. Conflicts with `name`.
* `user` - (Required) IAM user to which to attach this policy.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The user policy ID, in the form of `user_name:user_policy_name`.
* `name` - The name of the policy (always set).

## Import

```bash
ytofu import aws_iam_user_policy.mypolicy user_of_mypolicy_name:mypolicy_name
```
