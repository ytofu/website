# IAM Role Policy

Manage IAM Role Policy resources using ytofu YAML.

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
