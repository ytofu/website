# Resource: aws_ecr_pull_time_update_exclusion

Manages an AWS ECR (Elastic Container Registry) Pull Time Update Exclusion.

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

## Argument Reference

The following arguments are required:

* `principal_arn` - (Required, Forces new resource) ARN of the IAM principal to exclude from having image pull times recorded.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_ecr_pull_time_update_exclusion.example arn:aws:iam::123456789012:role/example-role
```
