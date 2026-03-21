# Lakeformation Resource

Manage Lakeformation Resource resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_s3_bucket:
    example:
      bucket: an-example-bucket

resource:
  aws_lakeformation_resource:
    example:
      arn: ${data.aws_s3_bucket.example.arn}
```
