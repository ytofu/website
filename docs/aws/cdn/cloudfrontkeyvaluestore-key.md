# Resource: aws_cloudfrontkeyvaluestore_key

ytofu resource for managing an AWS CloudFront KeyValueStore Key.

## Basic Example

```yaml
resource:
  aws_cloudfront_key_value_store:
    example:
      name: ExampleKeyValueStore
      comment: This is an example key value store

  aws_cloudfrontkeyvaluestore_key:
    example:
      key_value_store_arn: ${aws_cloudfront_key_value_store.example.arn}
      key: Test Key
      value: Test Value```

## Argument Reference

The following arguments are required:

* `key` - (Required) Key to put.
* `key_value_store_arn` - (Required) Amazon Resource Name (ARN) of the Key Value Store.
* `value` - (Required) Value to put.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Combination of attributes separated by a `,` to create a unique id: `key_value_store_arn`,`key`
* `total_size_in_bytes` - Total size of the Key Value Store in bytes.

## Import

```bash
ytofu import aws_cloudfrontkeyvaluestore_key.example arn:aws:cloudfront::111111111111:key-value-store/8562g61f-caba-2845-9d99-b97diwae5d3c,someKey
```
