# Resource: aws_iam_policy_attachment

Attaches a Managed IAM Policy to user(s), role(s), and/or group(s)

## Basic Example

```yaml
resource:
  aws_iam_user:
    user:
      name: test-user

  aws_iam_role:
    role:
      name: test-role
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

  aws_iam_group:
    group:
      name: test-group

  aws_iam_policy:
    policy:
      name: test-policy
      description: A test policy
      policy: ${data.aws_iam_policy_document.policy.json}

  aws_iam_policy_attachment:
    test-attach:
      name: test-attachment
      users: 
        - ${aws_iam_user.user.name}
      roles: 
        - ${aws_iam_role.role.name}
      groups: 
        - ${aws_iam_group.group.name}
      policy_arn: ${aws_iam_policy.policy.arn}

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
          - "*"```

## Argument Reference

This resource supports the following arguments:

* `name`    (Required) - Name of the attachment. This cannot be an empty string.
* `users`   (Optional) - User(s) the policy should be applied to.
* `roles`   (Optional) - Role(s) the policy should be applied to.
* `groups`  (Optional) - Group(s) the policy should be applied to.
* `policy_arn`  (Required) - ARN of the policy you want to apply. Typically this should be a reference to the ARN of another resource to ensure dependency ordering, such as `aws_iam_policy.example.arn`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Policy's ID.
* `name` - Name of the attachment.
