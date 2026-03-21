# ACM Certificate

Manage ACM Certificate resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_acm_certificate:
    cert:
      domain_name: example.com
      validation_method: DNS
      tags:
        Environment: test
      lifecycle:
        create_before_destroy: true
```

## Custom Domain Validation Options

```yaml
resource:
  aws_acm_certificate:
    cert:
      domain_name: testing.example.com
      validation_method: EMAIL
      validation_option:
        domain_name: testing.example.com
        validation_domain: example.com
```

## Existing Certificate Body Import

```yaml
resource:
  tls_private_key:
    example:
      algorithm: RSA

resource:
  tls_self_signed_cert:
    example:
      key_algorithm: RSA
      private_key_pem: ${tls_private_key.example.private_key_pem}
      subject:
        common_name: example.com
        organization: ACME Examples, Inc
      validity_period_hours: 12
      allowed_uses:
        - key_encipherment
        - digital_signature
        - server_auth

resource:
  aws_acm_certificate:
    cert:
      private_key: ${tls_private_key.example.private_key_pem}
      certificate_body: ${tls_self_signed_cert.example.cert_pem}
```

## DNS Validation with Route 53

```yaml
resource:
  aws_route53_record:
    example:
      allow_overwrite: true
      name: _acme-challenge.example.com
      records:
        - validation-token
      ttl: 60
      type: CNAME
      zone_id: ${aws_route53_zone.example.zone_id}
```
