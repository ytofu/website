# IAM User Policy

Manage IAM User Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iam_user_policy:
    lb_ro:
      name: test
      user: ${aws_iam_user.lb.name}
      policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": [ "ec2:Describe*", ] "Effect": "Allow" "Resource": "*" }, ] }'

resource:
  aws_iam_user:
    lb:
      name: loadbalancer
      path: /system/

resource:
  aws_iam_access_key:
    lb:
      user: ${aws_iam_user.lb.name}
```
