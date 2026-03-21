# Resource: aws_api_gateway_client_certificate

Provides an API Gateway Client Certificate.

## Basic Example

```yaml
resource:
  aws_api_gateway_client_certificate:
    demo:
      description: My client certificate
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) Description of the client certificate.
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Identifier of the client certificate.
* `created_date` - Date when the client certificate was created.
* `expiration_date` - Date when the client certificate will expire.
* `pem_encoded_certificate` - The PEM-encoded public key of the client certificate.
* `arn` - ARN
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_api_gateway_client_certificate.demo ab1cqe
```
