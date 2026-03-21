# Resource: aws_dms_certificate

Provides a DMS (Data Migration Service) certificate resource. DMS certificates can be created, deleted, and imported.

## Basic Example

```yaml
resource:
  aws_dms_certificate:
    test:
      certificate_id: test-dms-certificate-tf
      certificate_pem: ...
      tags:
        Name: test
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `certificate_id` - (Required) The certificate identifier.
* `certificate_pem` - (Optional) The contents of the .pem X.509 certificate file for the certificate. Either `certificate_pem` or `certificate_wallet` must be set.
* `certificate_wallet` - (Optional) The contents of the Oracle Wallet certificate for use with SSL, provided as a base64-encoded String. Either `certificate_pem` or `certificate_wallet` must be set.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `certificate_arn` - The Amazon Resource Name (ARN) for the certificate.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_dms_certificate.test test-dms-certificate-tf
```
