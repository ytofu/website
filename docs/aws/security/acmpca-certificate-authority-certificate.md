# Acmpca Certificate Authority Certificate

Manage Acmpca Certificate Authority Certificate resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_acmpca_certificate_authority_certificate:
    example:
      certificate_authority_arn: ${aws_acmpca_certificate_authority.example.arn}
      certificate: ${aws_acmpca_certificate.example.certificate}
      certificate_chain: ${aws_acmpca_certificate.example.certificate_chain}

resource:
  aws_acmpca_certificate:
    example:
      certificate_authority_arn: ${aws_acmpca_certificate_authority.example.arn}
      certificate_signing_request: ${aws_acmpca_certificate_authority.example.certificate_signing_request}
      signing_algorithm: SHA512WITHRSA
      template_arn: "arn:${data.aws_partition.current.partition}:acm-pca:::template/RootCACertificate/V1"
      validity:
        type: YEARS
        value: 1

resource:
  aws_acmpca_certificate_authority:
    example:
      type: ROOT
      certificate_authority_configuration:
        key_algorithm: RSA_4096
        signing_algorithm: SHA512WITHRSA
        subject:
          common_name: example.com

data:
  aws_partition:
    current:
```

## Certificate for Subordinate Certificate Authority

```yaml
resource:
  aws_acmpca_certificate_authority_certificate:
    subordinate:
      certificate_authority_arn: ${aws_acmpca_certificate_authority.subordinate.arn}
      certificate: ${aws_acmpca_certificate.subordinate.certificate}
      certificate_chain: ${aws_acmpca_certificate.subordinate.certificate_chain}

resource:
  aws_acmpca_certificate:
    subordinate:
      certificate_authority_arn: ${aws_acmpca_certificate_authority.root.arn}
      certificate_signing_request: ${aws_acmpca_certificate_authority.subordinate.certificate_signing_request}
      signing_algorithm: SHA512WITHRSA
      template_arn: "arn:${data.aws_partition.current.partition}:acm-pca:::template/SubordinateCACertificate_PathLen0/V1"
      validity:
        type: YEARS
        value: 1

resource:
  aws_acmpca_certificate_authority:
    subordinate:
      type: SUBORDINATE
      certificate_authority_configuration:
        key_algorithm: RSA_2048
        signing_algorithm: SHA512WITHRSA
        subject:
          common_name: sub.example.com

resource:
  aws_acmpca_certificate_authority:
    root:

resource:
  aws_acmpca_certificate_authority_certificate:
    root:

resource:
  aws_acmpca_certificate:
    root:

data:
  aws_partition:
    current:
```
