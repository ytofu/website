# Resource: aws_secretsmanager_secret_rotation

Provides a resource to manage AWS Secrets Manager secret rotation. To manage a secret, see the `aws_secretsmanager_secret` resource. To manage a secret value, see the `aws_secretsmanager_secret_version` resource.

## Basic Example

```yaml
resource:
  aws_secretsmanager_secret_rotation:
    example:
      secret_id: ${aws_secretsmanager_secret.example.id}
      rotation_lambda_arn: ${aws_lambda_function.example.arn}
      rotation_rules:
        automatically_after_days: 30
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `secret_id` - (Required) Specifies the secret to which you want to add a new version. You can specify either the Amazon Resource Name (ARN) or the friendly name of the secret. The secret must already exist.
* `rotate_immediately` - (Optional) Specifies whether to rotate the secret immediately or wait until the next scheduled rotation window. The rotation schedule is defined in `rotation_rules`. For secrets that use a Lambda rotation function to rotate, if you don't immediately rotate the secret, Secrets Manager tests the rotation configuration by running the testSecret step (https://docs.aws.amazon.com/secretsmanager/latest/userguide/rotate-secrets_how.html) of the Lambda rotation function. The test creates an AWSPENDING version of the secret and then removes it. Defaults to `true`.
* `rotation_lambda_arn` - (Optional) Specifies the ARN of the Lambda function that can rotate the secret. Must be supplied if the secret is not managed by AWS.
* `rotation_rules` - (Required) A structure that defines the rotation configuration for this secret. Defined below.

### rotation_rules

* `automatically_after_days` - (Optional) Specifies the number of days between automatic scheduled rotations of the secret. Either `automatically_after_days` or `schedule_expression` must be specified.
* `duration` - (Optional) - The length of the rotation window in hours. For example, `3h` for a three hour window.
* `schedule_expression` - (Optional) A `cron()` or `rate()` expression that defines the schedule for rotating your secret. Either `automatically_after_days` or `schedule_expression` must be specified.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Amazon Resource Name (ARN) of the secret.
* `arn` - Amazon Resource Name (ARN) of the secret.
* `rotation_enabled` - Specifies whether automatic rotation is enabled for this secret.

## Import

```bash
ytofu import aws_secretsmanager_secret_rotation.example arn:aws:secretsmanager:us-east-1:123456789012:secret:example-123456
```
