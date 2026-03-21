# Cloudfrontkeyvaluestore Keys Exclusive

Manage Cloudfrontkeyvaluestore Keys Exclusive resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudfront_key_value_store:
    example:
      name: ExampleKeyValueStore
      comment: This is an example key value store

resource:
  aws_cloudfrontkeyvaluestore_keys_exclusive:
    example:
      key_value_store_arn: ${aws_cloudfront_key_value_store.example.arn}
      resource_key_value_pair:
        key: Test Key
        value: Test Value
```

## Disallow Key Value Pairs

```yaml
resource:
  aws_cloudfrontkeyvaluestore_keys_exclusive:
    example:
      key_value_store_arn: ${aws_cloudfront_key_value_store.example.arn}
```
