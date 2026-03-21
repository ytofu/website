# Resource: aws_acm_certificate

The ACM certificate resource allows requesting and management of certificates
from the Amazon Certificate Manager.

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

  aws_acm_certificate:
    cert:
      private_key: ${tls_private_key.example.private_key_pem}
      certificate_body: ${tls_self_signed_cert.example.cert_pem}```

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* Creating an Amazon issued certificate
    * `domain_name` - (Required) Domain name for which the certificate should be issued
    * `subject_alternative_names` - (Optional) Set of domains that should be SANs in the issued certificate. To remove all elements of a previously configured list, set this value equal to an empty list (`[]`) or use the `ytofu taint` command to trigger recreation.
    * `validation_method` - (Optional) Which method to use for validation. `DNS` or `EMAIL` are valid. This parameter must not be set for certificates that were imported into ACM and then into ytofu.
    * `key_algorithm` - (Optional) Specifies the algorithm of the public and private key pair that your Amazon issued certificate uses to encrypt data. See [ACM Certificate characteristics](https://docs.aws.amazon.com/acm/latest/userguide/acm-certificate.html#algorithms) for more details.
    * `options` - (Optional) Configuration block used to set certificate options. Detailed below.
    * `validation_option` - (Optional) Configuration block used to specify information about the initial validation of each domain name. Detailed below.
* Importing an existing certificate
    * `private_key` - (Required) Certificate's PEM-formatted private key
    * `certificate_body` - (Required) Certificate's PEM-formatted public key
    * `certificate_chain` - (Optional) Certificate's PEM-formatted chain
* Creating a private CA issued certificate
    * `certificate_authority_arn` - (Required) ARN of an ACM PCA
    * `domain_name` - (Required) Domain name for which the certificate should be issued.
    * `early_renewal_duration` - (Optional) Amount of time to start automatic renewal process before expiration.
      Has no effect if less than 60 days.
      Represented by either
      a subset of [RFC 3339 duration](https://www.rfc-editor.org/rfc/rfc3339) supporting years, months, and days (e.g., `P90D`),
      or a string such as `2160h`.
    * `subject_alternative_names` - (Optional) Set of domains that should be SANs in the issued certificate.  To remove all elements of a previously configured list, set this value equal to an empty list (`[]`) or use the `ytofu taint` command to trigger recreation.
* `tags` - (Optional) Map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## options Configuration Block

Supported nested arguments for the `options` configuration block:

* `certificate_transparency_logging_preference` - (Optional) Whether certificate details should be added to a certificate transparency log. Valid values are `ENABLED` or `DISABLED`. See https://docs.aws.amazon.com/acm/latest/userguide/acm-concepts.html#concept-transparency for more details.
* `export` - (Optional) Whether the certificate can be exported. Valid values are `ENABLED` or `DISABLED` (default). **Note** Issuing an exportable certificate is subject to additional charges. See [AWS Certificate Manager pricing](https://aws.amazon.com/certificate-manager/pricing/) for more details.

## validation_option Configuration Block

Supported nested arguments for the `validation_option` configuration block:

* `domain_name` - (Required) Fully qualified domain name (FQDN) in the certificate.
* `validation_domain` - (Required) Domain name that you want ACM to use to send you validation emails. This domain name is the suffix of the email addresses that you want ACM to use. This must be the same as the `domain_name` value or a superdomain of the `domain_name` value. For example, if you request a certificate for `"testing.example.com"`, you can specify `"example.com"` for this value.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - ARN of the certificate
* `arn` - ARN of the certificate
* `domain_name` - Domain name for which the certificate is issued
* `domain_validation_options` - Set of domain validation objects which can be used to complete certificate validation.
  Can have more than one element, e.g., if SANs are defined.
  Only set if `DNS`-validation was used.
* `not_after` - Expiration date and time of the certificate.
* `not_before` - Start of the validity period of the certificate.
* `pending_renewal` - `true` if a Private certificate eligible for managed renewal is within the `early_renewal_duration` period.
* `renewal_eligibility` - Whether the certificate is eligible for managed renewal.
* `renewal_summary` - Contains information about the status of ACM's [managed renewal](https://docs.aws.amazon.com/acm/latest/userguide/acm-renewal.html) for the certificate.
* `status` - Status of the certificate.
* `type` - Source of the certificate.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
* `validation_emails` - List of addresses that received a validation email. Only set if `EMAIL` validation was used.

Domain validation objects export the following attributes:

* `domain_name` - Domain to be validated
* `resource_record_name` - The name of the DNS record to create to validate the certificate
* `resource_record_type` - The type of DNS record to create
* `resource_record_value` - The value the DNS record needs to have

Renewal summary objects export the following attributes:

* `renewal_status` - The status of ACM's managed renewal of the certificate
* `renewal_status_reason` - The reason that a renewal request was unsuccessful or is pending

[1]: https://www.terraform.io/docs/configuration/meta-arguments/lifecycle.html

## Import

```bash
ytofu import aws_acm_certificate.example arn:aws:acm:eu-central-1:123456789012:certificate/7e7a28d2-163f-4b8f-b9cd-822f96c08d6a
```
