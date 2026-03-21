# Cloudfront Trust Store

Manage Cloudfront Trust Store resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudfront_trust_store:
    example:
      name: example-trust-store
      ca_certificates_bundle_source:
        ca_certificates_bundle_s3_location:
          bucket: example-bucket
          key: ca-certificates.pem
          region: us-east-1
```

## With S3 Object Version

```yaml
resource:
  aws_cloudfront_trust_store:
    example:
      name: example-trust-store
      ca_certificates_bundle_source:
        ca_certificates_bundle_s3_location:
          bucket: example-bucket
          key: ca-certificates.pem
          region: us-east-1
          version: abc123
```
