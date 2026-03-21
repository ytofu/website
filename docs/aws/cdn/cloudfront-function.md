# Resource: aws_cloudfront_function

Provides a CloudFront Function resource. With CloudFront Functions in Amazon CloudFront, you can write lightweight functions in JavaScript for high-scale, latency-sensitive CDN customizations.

## Basic Example

```yaml
resource:
  aws_cloudfront_function:
    test:
      name: test
      runtime: cloudfront-js-2.0
      comment: my function
      publish: true
      code: file-content
```

## Argument Reference

The following arguments are required:

* `name` - (Required) Unique name for your CloudFront Function.
* `code` - (Required) Source code of the function
* `runtime` - (Required) Identifier of the function's runtime. Valid values are `cloudfront-js-1.0` and `cloudfront-js-2.0`.

The following arguments are optional:

* `comment` - (Optional) Comment.
* `publish` - (Optional) Whether to publish creation/change as Live CloudFront Function Version. Defaults to `true`.
* `key_value_store_associations` - (Optional) List of `aws_cloudfront_key_value_store` ARNs to be associated to the function. AWS limits associations to one key value store per function.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) identifying your CloudFront Function.
* `etag` - ETag hash of the function. This is the value for the `DEVELOPMENT` stage of the function.
* `live_stage_etag` - ETag hash of any `LIVE` stage of the function.
* `status` - Status of the function. Can be `UNPUBLISHED`, `UNASSOCIATED` or `ASSOCIATED`.

## Import

```bash
ytofu import aws_cloudfront_function.test my_test_function
```
