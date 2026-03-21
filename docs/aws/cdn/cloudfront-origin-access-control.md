# Cloudfront Origin Access Control

Manage Cloudfront Origin Access Control resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudfront_origin_access_control:
    example:
      name: example
      description: Example Policy
      origin_access_control_origin_type: s3
      signing_behavior: always
      signing_protocol: sigv4
```
