# Resource: aws_acmpca_certificate_authority_certificate

Associates a certificate with an AWS Certificate Manager Private Certificate Authority (ACM PCA Certificate Authority). An ACM PCA Certificate Authority is unable to issue certificates until it has a certificate associated with it. A root level ACM PCA Certificate Authority is able to self-sign its own root certificate.

## Basic Example

```yaml
resource:
  aws_acmpca_certificate_authority_certificate:
    example:
      certificate_authority_arn: ${aws_acmpca_certificate_authority.example.arn}
      certificate: ${aws_acmpca_certificate.example.certificate}
      certificate_chain: ${aws_acmpca_certificate.example.certificate_chain}

  aws_acmpca_certificate:
    example:
      certificate_authority_arn: ${aws_acmpca_certificate_authority.example.arn}
      certificate_signing_request: ${aws_acmpca_certificate_authority.example.certificate_signing_request}
      signing_algorithm: SHA512WITHRSA
      template_arn: "arn:${data.aws_partition.current.partition}:acm-pca:::template/RootCACertificate/V1"
      validity:
        type: YEARS
        value: 1

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
    current:```

## Certificate for Subordinate Certificate Authority

```yaml
resource:
  aws_acmpca_certificate_authority_certificate:
    subordinate:
      certificate_authority_arn: ${aws_acmpca_certificate_authority.subordinate.arn}
      certificate: ${aws_acmpca_certificate.subordinate.certificate}
      certificate_chain: ${aws_acmpca_certificate.subordinate.certificate_chain}

  aws_acmpca_certificate:
    subordinate:
      certificate_authority_arn: ${aws_acmpca_certificate_authority.root.arn}
      certificate_signing_request: ${aws_acmpca_certificate_authority.subordinate.certificate_signing_request}
      signing_algorithm: SHA512WITHRSA
      template_arn: "arn:${data.aws_partition.current.partition}:acm-pca:::template/SubordinateCACertificate_PathLen0/V1"
      validity:
        type: YEARS
        value: 1

  aws_acmpca_certificate_authority:
    subordinate:
      type: SUBORDINATE
      certificate_authority_configuration:
        key_algorithm: RSA_2048
        signing_algorithm: SHA512WITHRSA
        subject:
          common_name: sub.example.com

  aws_acmpca_certificate_authority:
    root:

  aws_acmpca_certificate_authority_certificate:
    root:

  aws_acmpca_certificate:
    root:

data:
  aws_partition:
    current:```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `certificate` - (Required) PEM-encoded certificate for the Certificate Authority.
* `certificate_authority_arn` - (Required) ARN of the Certificate Authority.
* `certificate_chain` - (Optional) PEM-encoded certificate chain that includes any intermediate certificates and chains up to root CA. Required for subordinate Certificate Authorities. Not allowed for root Certificate Authorities.

## Attribute Reference

This resource exports no additional attributes.
