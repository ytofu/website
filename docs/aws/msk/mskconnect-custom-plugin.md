# Mskconnect Custom Plugin

Manage Mskconnect Custom Plugin resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: example

resource:
  aws_s3_object:
    example:
      bucket: ${aws_s3_bucket.example.id}
      key: debezium.zip
      source: debezium.zip

resource:
  aws_mskconnect_custom_plugin:
    example:
      name: debezium-example
      content_type: ZIP
      location:
        s3:
          bucket_arn: ${aws_s3_bucket.example.arn}
          file_key: ${aws_s3_object.example.key}
```
