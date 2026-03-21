# Resource: aws_cloud9_environment_membership

Provides an environment member to an AWS Cloud9 development environment.

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `environment_id` - (Required) The ID of the environment that contains the environment member you want to add.
* `permissions` - (Required) The type of environment member permissions you want to associate with this environment member. Allowed values are `read-only` and `read-write` .
* `user_arn` - (Required) The Amazon Resource Name (ARN) of the environment member you want to add.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the environment membership.
* `user_id` - The user ID in AWS Identity and Access Management (AWS IAM) of the environment member.

## Import

```bash
ytofu import aws_cloud9_environment_membership.test environment-id#user-arn
```
