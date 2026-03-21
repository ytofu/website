# ECR Pull Time Update Exclusion

Manage ECR Pull Time Update Exclusion resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iam_role:
    example:
      name: example-role
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": "sts:AssumeRole" "Effect": "Allow" "Principal": { "Service": "ec2.amazonaws.com" } } ] }'

resource:
  aws_iam_role_policy:
    example:
      name: example-role-policy
      role: ${aws_iam_role.example.id}
      policy: '{ "Version": "2012-10-17" "Statement": [ { "Effect": "Allow" "Action": [ "ecr:GetAuthorizationToken", "ecr:BatchCheckLayerAvailability", "ecr:GetDownloadUrlForLayer", "ecr:BatchGetImage" ] "Resource": "*" } ] }'

resource:
  aws_ecr_pull_time_update_exclusion:
    example:
      principal_arn: ${aws_iam_role.example.arn}
```

## With IAM User

```yaml
resource:
  aws_iam_user:
    example:
      name: example-user

resource:
  aws_iam_user_policy:
    example:
      name: example-user-policy
      user: ${aws_iam_user.example.name}
      policy: '{ "Version": "2012-10-17" "Statement": [ { "Effect": "Allow" "Action": [ "ecr:GetAuthorizationToken", "ecr:BatchCheckLayerAvailability", "ecr:GetDownloadUrlForLayer", "ecr:BatchGetImage" ] "Resource": "*" } ] }'

resource:
  aws_ecr_pull_time_update_exclusion:
    example:
      principal_arn: ${aws_iam_user.example.arn}
```
