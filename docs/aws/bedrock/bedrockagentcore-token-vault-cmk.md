# Resource: aws_bedrockagentcore_token_vault_cmk

Manages the AWS KMS customer master key (CMK) for a token vault.

## Basic Example

```yaml
resource:
  aws_bedrockagentcore_token_vault_cmk:
    example:
      kms_configuration:
        key_type: CustomerManagedKey
        kms_key_arn: ${aws_kms_key.example.arn}
```

## Argument Reference

This resource supports the following arguments:

* `kms_configuration` - (Required) KMS configuration for the token vault. See [`kms_configuration`](#kms_configuration) below.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `token_vault_id` - (Optional) Token vault ID. Defaults to `default`.

### `kms_configuration`

The `kms_configuration` block supports the following:

* `key_type` - (Required) Type of KMS key. Valid values: `CustomerManagedKey`, `ServiceManagedKey`.
* `kms_key_arn` - (Optional) ARN of the KMS key.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_bedrockagentcore_token_vault_cmk.example "default"
```
