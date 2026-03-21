# Bedrockagentcore Token Vault Cmk

Manage Bedrockagentcore Token Vault Cmk resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_bedrockagentcore_token_vault_cmk:
    example:
      kms_configuration:
        key_type: CustomerManagedKey
        kms_key_arn: ${aws_kms_key.example.arn}
```
