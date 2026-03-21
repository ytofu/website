# IAM Server Certificate

Manage IAM Server Certificate resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iam_server_certificate:
    test_cert:
      name: some_test_cert
      certificate_body: file-content
      private_key: file-content
```
