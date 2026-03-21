# Resource: aws_secretsmanager_secret_version

Provides a resource to manage AWS Secrets Manager secret version including its secret value. To manage secret metadata, see the `aws_secretsmanager_secret` resource.

## Basic Example

```yaml
resource:
  aws_secretsmanager_secret_version:
    example:
      secret_id: ${aws_secretsmanager_secret.example.id}
      secret_string: example-string-to-protect
```

## Key-Value Pairs

```yaml
resource:
  aws_secretsmanager_secret_version:
    example:
      secret_id: ${aws_secretsmanager_secret.example.id}
      secret_string: example-value
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `secret_id` - (Required) Specifies the secret to which you want to add a new version. You can specify either the Amazon Resource Name (ARN) or the friendly name of the secret. The secret must already exist.
* `secret_string` - (Optional) Specifies text data that you want to encrypt and store in this version of the secret. This is required if `secret_binary` or `secret_string_wo` is not set.
* `secret_string_wo` - (Optional) Specifies text data that you want to encrypt and store in this version of the secret. This is required if `secret_binary` or `secret_string` is not set.
* `secret_string_wo_version`  - (Optional) Used together with `secret_string_wo` to trigger an update. Increment this value when an update to `secret_string_wo` is required.
* `secret_binary` - (Optional) Specifies binary data that you want to encrypt and store in this version of the secret. This is required if `secret_string` or `secret_string_wo` is not set. Needs to be encoded to base64.
* `version_stages` - (Optional) Specifies a list of staging labels that are attached to this version of the secret. A staging label must be unique to a single version of the secret. If you specify a staging label that's already associated with a different version of the same secret then that staging label is automatically removed from the other version and attached to this version. If you do not specify a value, then AWS Secrets Manager automatically moves the staging label `AWSCURRENT` to this new version on creation.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The ARN of the secret.
* `id` - A pipe delimited combination of secret ID and version ID.
* `version_id` - The unique identifier of the version of the secret.

## Import

```bash
ytofu import aws_secretsmanager_secret_version.example 'arn:aws:secretsmanager:us-east-1:123456789012:secret:example-123456|xxxxx-xxxxxxx-xxxxxxx-xxxxx'
```
