# Paymentcryptography Key Alias

Manage Paymentcryptography Key Alias resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_paymentcryptography_key:
    test:
      exportable: true
      key_attributes:
        key_algorithm: TDES_3KEY
        key_class: SYMMETRIC_KEY
        key_usage: TR31_P0_PIN_ENCRYPTION_KEY
        key_modes_of_use:
          decrypt: true
          encrypt: true
          wrap: true
          unwrap: true

resource:
  aws_paymentcryptography_key_alias:
    test:
      alias_name: alias/test-alias
      key_arn: ${aws_paymentcryptography_key.test.arn}
```
