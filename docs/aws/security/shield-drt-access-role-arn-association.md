# Shield Drt Access Role ARN Association

Manage Shield Drt Access Role ARN Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_shield_drt_access_role_arn_association:
    example:
      role_arn: ${aws_iam_role.example.arn}

resource:
  aws_iam_role:
    example:
      name: example-role
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Sid" : "", "Effect" : "Allow", "Principal" : { "Service" : "drt.shield.amazonaws.com" }, "Action" : "sts:AssumeRole" }, ] }'

resource:
  aws_iam_role_policy_attachment:
    example:
      role: ${aws_iam_role.example.name}
      policy_arn: "arn:aws:iam::aws:policy/service-role/AWSShieldDRTAccessPolicy"
```
