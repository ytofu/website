# S3 Bucket Website Configuration

Manage S3 Bucket Website Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket_website_configuration:
    example:
      bucket: ${aws_s3_bucket.example.id}
      index_document:
        suffix: index.html
      error_document:
        key: error.html
      routing_rule:
        condition:
          key_prefix_equals: docs/
        redirect:
          replace_key_prefix_with: documents/
```

## With `routing_rules` configured

```yaml
resource:
  aws_s3_bucket_website_configuration:
    example:
      bucket: ${aws_s3_bucket.example.id}
      index_document:
        suffix: index.html
      error_document:
        key: error.html
      routing_rules: |
        [{
        "Condition": {
        "KeyPrefixEquals": "docs/"
        },
        "Redirect": {
        "ReplaceKeyPrefixWith": ""
        }
        }]
```
