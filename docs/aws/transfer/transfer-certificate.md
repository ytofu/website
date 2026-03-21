# Resource: aws_transfer_certificate

Provides a AWS Transfer AS2 Certificate resource.

## Basic Example

```yaml
resource:
  aws_transfer_certificate:
    example:
      certificate: file-content
      certificate_chain: file-content
      private_key: file-content
      description: example
      usage: SIGNING
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `certificate` - (Required) The valid certificate file required for the transfer.
* `certificate_chain` - (Optional) The optional list of certificate that make up the chain for the certificate that is being imported.
* `description` - (Optional) A short description that helps identify the certificate.
* `private_key` - (Optional) The private key associated with the certificate being imported.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `usage` - (Required) Specifies if a certificate is being used for signing or encryption. The valid values are SIGNING and ENCRYPTION.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The ARN of the certificate
* `certificate_id` - The unique identifier for the AS2 certificate
* `active_date` - An date when the certificate becomes active
* `inactive_date` - An date when the certificate becomes inactive

## Import

```bash
ytofu import aws_transfer_certificate.example c-4221a88afd5f4362a
```
