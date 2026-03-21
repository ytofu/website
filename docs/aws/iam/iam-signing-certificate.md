# IAM Signing Certificate

Manage IAM Signing Certificate resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iam_signing_certificate:
    test_cert:
      username: some_test_cert
      certificate_body: file-content
```
