# Rolesanywhere Trust Anchor

Manage Rolesanywhere Trust Anchor resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_acmpca_certificate_authority:
    example:
      permanent_deletion_time_in_days: 7
      type: ROOT
      certificate_authority_configuration:
        key_algorithm: RSA_4096
        signing_algorithm: SHA512WITHRSA
        subject:
          common_name: example.com

data:
  aws_partition:
    current:

resource:
  aws_acmpca_certificate:
    test:
      certificate_authority_arn: ${aws_acmpca_certificate_authority.example.arn}
      certificate_signing_request: ${aws_acmpca_certificate_authority.example.certificate_signing_request}
      signing_algorithm: SHA512WITHRSA
      template_arn: "arn:${data.aws_partition.current.partition}:acm-pca:::template/RootCACertificate/V1"
      validity:
        type: YEARS
        value: 1

resource:
  aws_acmpca_certificate_authority_certificate:
    example:
      certificate_authority_arn: ${aws_acmpca_certificate_authority.example.arn}
      certificate: ${aws_acmpca_certificate.example.certificate}
      certificate_chain: ${aws_acmpca_certificate.example.certificate_chain}

resource:
  aws_rolesanywhere_trust_anchor:
    test:
      name: example
      source:
        source_data:
          acm_pca_arn: ${aws_acmpca_certificate_authority.example.arn}
        source_type: AWS_ACM_PCA
      depends_on: 
        - ${aws_acmpca_certificate_authority_certificate.example}
```
