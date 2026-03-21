# Cloud9 Environment Membership

Manage Cloud9 Environment Membership resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloud9_environment_ec2:
    test:
      instance_type: t2.micro
      name: some-env

resource:
  aws_iam_user:
    test:
      name: some-user

resource:
  aws_cloud9_environment_membership:
    test:
      environment_id: ${aws_cloud9_environment_ec2.test.id}
      permissions: read-only
      user_arn: ${aws_iam_user.test.arn}
```
