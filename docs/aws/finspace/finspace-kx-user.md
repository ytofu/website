# Finspace Kx User

Manage Finspace Kx User resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_kms_key:
    example:
      description: Example KMS Key
      deletion_window_in_days: 7

resource:
  aws_finspace_kx_environment:
    example:
      name: my-tf-kx-environment
      kms_key_id: ${aws_kms_key.example.arn}

resource:
  aws_iam_role:
    example:
      name: example-role
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": "sts:AssumeRole" "Effect": "Allow" "Sid": "" "Principal": { "Service": "ec2.amazonaws.com" } }, ] }'

resource:
  aws_finspace_kx_user:
    example:
      name: my-tf-kx-user
      environment_id: ${aws_finspace_kx_environment.example.id}
      iam_role: ${aws_iam_role.example.arn}
```
