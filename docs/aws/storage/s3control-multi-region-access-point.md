# S3control Multi Region Access Point

Manage S3control Multi Region Access Point resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    foo_bucket:
      bucket: example-bucket-foo

resource:
  aws_s3_bucket:
    bar_bucket:
      bucket: example-bucket-bar

resource:
  aws_s3control_multi_region_access_point:
    example:
      details:
        name: example
        region:
          bucket: ${aws_s3_bucket.foo_bucket.id}
        region:
          bucket: ${aws_s3_bucket.bar_bucket.id}
```
