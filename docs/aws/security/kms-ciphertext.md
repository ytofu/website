# KMS Ciphertext

Manage KMS Ciphertext resources using ytofu YAML.

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
