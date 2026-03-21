# Resource: aws_rolesanywhere_trust_anchor

ytofu resource for managing a Roles Anywhere Trust Anchor.

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

## Argument Reference

This resource supports the following arguments:

* `enabled` - (Optional) Whether or not the Trust Anchor should be enabled.
* `name` - (Required) The name of the Trust Anchor.
* `source` - (Required) The source of trust, documented below
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### Nested Blocks

#### `source`

* `source_data` - (Required) The data denoting the source of trust, documented below
* `source_type` - (Required) The type of the source of trust. Must be either `AWS_ACM_PCA` or `CERTIFICATE_BUNDLE`.

#### `source_data`

* `acm_pca_arn` - (Optional, required when `source_type` is `AWS_ACM_PCA`) The ARN of an ACM Private Certificate Authority.
* `x509_certificate_data` - (Optional, required when `source_type` is `CERTIFICATE_BUNDLE`)

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) of the Trust Anchor
* `id` - The Trust Anchor ID.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_rolesanywhere_trust_anchor.example 92b2fbbb-984d-41a3-a765-e3cbdb69ebb1
```
