# Resource: aws_cloudfront_key_value_store

ytofu resource for managing an AWS CloudFront Key Value Store.

## Basic Example

```yaml
resource:
  aws_cloudfront_key_value_store:
    example:
      name: ExampleKeyValueStore
      comment: This is an example key value store
```

## Argument Reference

The following arguments are required:

* `name` - (Required) Unique name for your CloudFront KeyValueStore.

The following arguments are optional:

* `comment` - (Optional) Comment.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) identifying your CloudFront KeyValueStore.
* `etag` - ETag hash of the KeyValueStore.
* `id` - A unique identifier for the KeyValueStore.

## Timeouts

Configuration options:

* `create` - (Default `30m`)

## Import

```bash
ytofu import aws_cloudfront_key_value_store.example example_store
```
