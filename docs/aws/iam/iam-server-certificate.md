# Resource: aws_iam_server_certificate

Provides an IAM Server Certificate resource to upload Server Certificates.
Certs uploaded to IAM can easily work with other AWS services such as:

## Basic Example

```yaml
resource:
  aws_iam_server_certificate:
    test_cert:
      name: some_test_cert
      certificate_body: file-content
      private_key: file-content
```

## Argument Reference

This resource supports the following arguments:

* `certificate_body` - (Required, Forces new resource) The contents of the public key certificate in
  PEM-encoded format.
* `certificate_chain` - (Optional, Forces new resource) The contents of the certificate chain.
  This is typically a concatenation of the PEM-encoded public key certificates
  of the chain.
* `name` - (Optional) The name of the Server Certificate. Do not include the path in this value. If omitted, ytofu will assign a random, unique name.
* `name_prefix` - (Optional) Creates a unique name beginning with the specified
  prefix. Conflicts with `name`.
* `path` - (Optional) The IAM path for the server certificate.  If it is not
    included, it defaults to a slash (/). If this certificate is for use with
    AWS CloudFront, the path must be in format `/cloudfront/your_path_here`.
    See [IAM Identifiers][1] for more details on IAM Paths.
* `private_key` - (Required, Forces new resource) The contents of the private key in PEM-encoded format.
* `tags` - (Optional) Map of resource tags for the server certificate. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The Amazon Resource Name (ARN) specifying the server certificate.
* `expiration` - Date and time in [RFC3339 format](https://tools.ietf.org/html/rfc3339#section-5.8) on which the certificate is set to expire.
* `id` - The unique Server Certificate name
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
* `upload_date` - Date and time in [RFC3339 format](https://tools.ietf.org/html/rfc3339#section-5.8) when the server certificate was uploaded.

## Timeouts

Configuration options:

- `delete` - (Default `15m`)

## Import

```bash
ytofu import aws_iam_server_certificate.certificate example.com-certificate-until-2018
```
