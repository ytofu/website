# Resource: aws_kms_ciphertext

The KMS ciphertext resource allows you to encrypt plaintext into ciphertext
by using an AWS KMS customer master key. The value returned by this resource
is stable across every apply. For a changing ciphertext value each apply, see
the `aws_kms_ciphertext` data source.

## Basic Example

```yaml
resource:
  aws_kms_key:
    oauth_config:
      description: oauth config
      is_enabled: true

resource:
  aws_kms_ciphertext:
    oauth:
      key_id: ${aws_kms_key.oauth_config.key_id}
      plaintext: |
        {
        "client_id": "e587dbae22222f55da22",
        "client_secret": "8289575d00000ace55e1815ec13673955721b8a5"
        }
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `plaintext` - (Exactly one of `plaintext` or `plaintext_wo` must be set) Data to be encrypted. Note that this may show up in logs, and it will be stored in the state file.
* `plaintext_wo` - (Write-Only, Exactly one of `plaintext` or `plaintext_wo` must be set) Data to be encrypted. Note that this may show up in logs. It will not be stored in the state file.
* `plaintext_wo_version` - (Required when `plaintext_wo` is set) Used together with `plaintext_wo` to trigger a replacement. Modify this value when a replacement is required.
* `key_id` - (Required) Globally unique key ID for the customer master key.
* `context` - (Optional) An optional mapping that makes up the encryption context.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `ciphertext_blob` - Base64 encoded ciphertext
