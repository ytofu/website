# Resource: aws_iam_role_policy_attachment

Attaches a Managed IAM Policy to an IAM role

## Basic Example

```yaml
data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - ec2.amazonaws.com
        actions: 
          - "sts:AssumeRole"

  aws_iam_policy_document:
    policy:
      statement:
        effect: Allow
        actions: 
          - "ec2:Describe*"
        resources: 
          - "*"

resource:
  aws_iam_role:
    role:
      name: test-role
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

  aws_iam_policy:
    policy:
      name: test-policy
      description: A test policy
      policy: ${data.aws_iam_policy_document.policy.json}

  aws_iam_role_policy_attachment:
    test-attach:
      role: ${aws_iam_role.role.name}
      policy_arn: ${aws_iam_policy.policy.arn}```

## Argument Reference

This resource supports the following arguments:

* `role`  (Required) - The name of the IAM role to which the policy should be applied
* `policy_arn` (Required) - The ARN of the policy you want to apply

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_iam_role_policy_attachment.example test-role/arn:aws:iam::xxxxxxxxxxxx:policy/test-policy
```
