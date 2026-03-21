# Resource: aws_redshift_hsm_client_certificate

Creates an HSM client certificate that an Amazon Redshift cluster will use to connect to the client's HSM in order to store and retrieve the keys used to encrypt the cluster databases.

## Basic Example

```yaml
resource:
  aws_redshift_hsm_client_certificate:
    example:
      hsm_client_certificate_identifier: example
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `hsm_client_certificate_identifier` - (Required, Forces new resource) The identifier of the HSM client certificate.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) of the Hsm Client Certificate.
* `hsm_client_certificate_public_key` - The public key that the Amazon Redshift cluster will use to connect to the HSM. You must register the public key in the HSM.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_redshift_hsm_client_certificate.test example
```
