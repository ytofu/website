# Resource: aws_cloudfrontkeyvaluestore_keys_exclusive

ytofu resource for maintaining exclusive management of resource key value pairs defined in an AWS CloudFront KeyValueStore.

## Basic Example

```yaml
resource:
  aws_cloudfront_key_value_store:
    example:
      name: ExampleKeyValueStore
      comment: This is an example key value store

  aws_cloudfrontkeyvaluestore_keys_exclusive:
    example:
      key_value_store_arn: ${aws_cloudfront_key_value_store.example.arn}
      resource_key_value_pair:
        key: Test Key
        value: Test Value```

## Disallow Key Value Pairs

```yaml
resource:
  aws_cloudfrontkeyvaluestore_keys_exclusive:
    example:
      key_value_store_arn: ${aws_cloudfront_key_value_store.example.arn}
```

## Argument Reference

The following arguments are required:

* `key_value_store_arn` - (Required) Amazon Resource Name (ARN) of the Key Value Store.

The following arguments are optional:

* `max_batch_size` - (Optional) Maximum resource key values pairs that will update in a single API request. AWS has a default quota of 50 keys or a 3 MB payload, whichever is reached first. Defaults to `50`.
* `resource_key_value_pair` - (Optional) A list of all resource key value pairs associated with the KeyValueStore.
See [`resource_key_value_pair`](#resource_key_value_pair) below.

### `resource_key_value_pair`

The following arguments are required:

* `key` - (Required) Key to put.
* `value` - (Required) Value to put.

## Attribute Reference

This resource exports no additional attributes.

* `total_size_in_bytes` - Total size of the Key Value Store in bytes.

## Import

```bash
ytofu import aws_cloudfrontkeyvaluestore_keys_exclusive.example arn:aws:cloudfront::111111111111:key-value-store/8562g61f-caba-2845-9d99-b97diwae5d3c
```
