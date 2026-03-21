# Signer Signing Profile

Manage Signer Signing Profile resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_signer_signing_profile:
    test_sp:
      platform_id: AWSLambda-SHA384-ECDSA

resource:
  aws_signer_signing_profile:
    prod_sp:
      platform_id: AWSLambda-SHA384-ECDSA
      name_prefix: prod_sp_
      signature_validity_period:
        value: 5
        type: YEARS
      tags:
        tag1: value1
        tag2: value2
```
