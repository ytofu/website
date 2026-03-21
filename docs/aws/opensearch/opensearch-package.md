# Opensearch Package

Manage Opensearch Package resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    my_opensearch_packages:
      bucket: my-opensearch-packages

resource:
  aws_s3_object:
    example:
      bucket: ${aws_s3_bucket.my_opensearch_packages.bucket}
      key: example.txt
      source: ./example.txt
      etag: ${filemd5("./example.txt")}

resource:
  aws_opensearch_package:
    example:
      package_name: example-txt
      package_source:
        s3_bucket_name: ${aws_s3_bucket.my_opensearch_packages.bucket}
        s3_key: ${aws_s3_object.example.key}
      package_type: TXT-DICTIONARY
```
