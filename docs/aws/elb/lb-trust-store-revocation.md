# LB Trust Store Revocation

Manage LB Trust Store Revocation resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lb_trust_store:
    test:
      name: tf-example-lb-ts
      ca_certificates_bundle_s3_bucket: ...
      ca_certificates_bundle_s3_key: ...

resource:
  aws_lb_trust_store_revocation:
    test:
      trust_store_arn: ${aws_lb_trust_store.test.arn}
      revocations_s3_bucket: ...
      revocations_s3_key: ...
```
