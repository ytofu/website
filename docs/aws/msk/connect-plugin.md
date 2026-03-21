# MSK Connect Custom Plugin

Create Kafka Connect custom plugins using ytofu YAML.

## Basic Plugin

```yaml
resource:
  aws_mskconnect_custom_plugin:
    example:
      name: example
      content_type: ZIP
      location:
        s3:
          bucket_arn: ${aws_s3_bucket.example.arn}
          file_key: plugins/my-connector.zip
```
