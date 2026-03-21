# Resource: aws_iam_signing_certificate

Provides an IAM Signing Certificate resource to upload Signing Certificates.

## Basic Example

```yaml
resource:
  aws_iam_signing_certificate:
    test_cert:
      username: some_test_cert
      certificate_body: file-content
```

## Argument Reference

This resource supports the following arguments:

* `certificate_body` - (Required) The contents of the signing certificate in PEM-encoded format.
* `status` - (Optional)  The status you want to assign to the certificate. `Active` means that the certificate can be used for programmatic calls to Amazon Web Services `Inactive` means that the certificate cannot be used.
* `user_name` - (Required) The name of the user the signing certificate is for.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `certificate_id` - The ID for the signing certificate.
* `id` - The `certificate_id:user_name`

## Import

```bash
ytofu import aws_iam_signing_certificate.certificate IDIDIDIDID:user-name
```
