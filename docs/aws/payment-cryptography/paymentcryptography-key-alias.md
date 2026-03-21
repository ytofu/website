# Resource: aws_paymentcryptography_key_alias

ytofu resource for managing an AWS Payment Cryptography Control Plane Key Alias.

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

## Argument Reference

The following arguments are required:

* `alias_name` - (Required) Name of the Key Alias.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `key_arn` - (Optional) ARN of the key.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_paymentcryptography_key_alias.example alias/4681482429376900170
```
