# Cloudfront Function

Manage Cloudfront Function resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudfront_function:
    test:
      name: test
      runtime: cloudfront-js-2.0
      comment: my function
      publish: true
      code: file-content
```
