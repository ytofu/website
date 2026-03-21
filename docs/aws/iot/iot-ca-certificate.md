# IOT Ca Certificate

Manage IOT Ca Certificate resources using ytofu YAML.

## Basic Example

```yaml
resource:
  tls_self_signed_cert:
    ca:
      private_key_pem: ${tls_private_key.ca.private_key_pem}
      subject:
        common_name: example.com
        organization: ACME Examples, Inc
      validity_period_hours: 12
      allowed_uses:
        - key_encipherment
        - digital_signature
        - server_auth
      is_ca_certificate: true

resource:
  tls_private_key:
    ca:
      algorithm: RSA

resource:
  tls_cert_request:
    verification:
      private_key_pem: ${tls_private_key.verification.private_key_pem}
      subject:
        common_name: ${data.aws_iot_registration_code.example.registration_code}

resource:
  tls_private_key:
    verification:
      algorithm: RSA

resource:
  tls_locally_signed_cert:
    verification:
      cert_request_pem: ${tls_cert_request.verification.cert_request_pem}
      ca_private_key_pem: ${tls_private_key.ca.private_key_pem}
      ca_cert_pem: ${tls_self_signed_cert.ca.cert_pem}
      validity_period_hours: 12
      allowed_uses:
        - key_encipherment
        - digital_signature
        - server_auth

resource:
  aws_iot_ca_certificate:
    example:
      active: true
      ca_certificate_pem: ${tls_self_signed_cert.ca.cert_pem}
      verification_certificate_pem: ${tls_locally_signed_cert.verification.cert_pem}
      allow_auto_registration: true

data:
  aws_iot_registration_code:
    example:
```
