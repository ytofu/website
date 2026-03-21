# IAM Group Policy

Manage IAM Group Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iam_group_policy:
    my_developer_policy:
      name: my_developer_policy
      group: ${aws_iam_group.my_developers.name}
      policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": [ "ec2:Describe*", ] "Effect": "Allow" "Resource": "*" }, ] }'

resource:
  aws_iam_group:
    my_developers:
      name: developers
      path: /users/
```
