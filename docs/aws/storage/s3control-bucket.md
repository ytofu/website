# S3control Bucket

Manage S3control Bucket resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3control_bucket:
    example:
      bucket: example
      outpost_id: ${data.aws_outposts_outpost.example.id}
```
