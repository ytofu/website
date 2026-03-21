# Acmpca Certificate

Manage Acmpca Certificate resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_acmpca_certificate:
    example:
      certificate_authority_arn: ${aws_acmpca_certificate_authority.example.arn}
      certificate_signing_request: ${tls_cert_request.csr.cert_request_pem}
      signing_algorithm: SHA256WITHRSA
      validity:
        type: YEARS
        value: 1

resource:
  aws_acmpca_certificate_authority:
    example:
      certificate_authority_configuration:
        key_algorithm: RSA_4096
        signing_algorithm: SHA512WITHRSA
        subject:
          common_name: example.com
      permanent_deletion_time_in_days: 7

resource:
  tls_private_key:
    key:
      algorithm: RSA

resource:
  tls_cert_request:
    csr:
      private_key_pem: ${tls_private_key.key.private_key_pem}
      subject:
        common_name: example
```
