# OpenSearch Package

Deploy custom packages to OpenSearch domains using ytofu YAML.

## Basic Package

```yaml
resource:
  aws_opensearch_package:
    example:
      package_name: example-package
      package_source:
        s3_bucket_name: ${aws_s3_bucket.example.bucket}
        s3_key: packages/synonym.txt
      package_type: TXT-DICTIONARY
```
