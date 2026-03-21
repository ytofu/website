# Rolesanywhere Profile

Manage Rolesanywhere Profile resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iam_role:
    test:
      name: test
      path: /
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [{ "Action": [ "sts:AssumeRole", "sts:TagSession", "sts:SetSourceIdentity" ] "Principal": { "Service": "rolesanywhere.amazonaws.com", } "Effect": "Allow" "Sid": "" }] }'

resource:
  aws_rolesanywhere_profile:
    test:
      name: example
      role_arns: 
        - ${aws_iam_role.test.arn}
```
