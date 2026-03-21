# Acmpca Permission

Manage Acmpca Permission resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_acmpca_permission:
    example:
      certificate_authority_arn: ${aws_acmpca_certificate_authority.example.arn}
      actions: 
        - IssueCertificate
        - GetCertificate
        - ListPermissions
      principal: acm.amazonaws.com

resource:
  aws_acmpca_certificate_authority:
    example:
      certificate_authority_configuration:
        key_algorithm: RSA_4096
        signing_algorithm: SHA512WITHRSA
        subject:
          common_name: example.com
```
