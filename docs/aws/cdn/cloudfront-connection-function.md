# Resource: aws_cloudfront_connection_function

Manages an AWS CloudFront Connection Function.

## Basic Example

```yaml
resource:
  aws_cloudfront_connection_function:
    example:
      name: example-connection-function
      connection_function_code: "function handler(event) { return event.request; }"
      connection_function_config:
        runtime: cloudfront-js-2.0
        comment: Example connection function
```

## With Publish Enabled

```yaml
resource:
  aws_cloudfront_connection_function:
    example:
      name: example-connection-function
      connection_function_code: "function handler(event) { return event.request; }"
      connection_function_config:
        runtime: cloudfront-js-2.0
        comment: Example connection function
      publish: true
```

## With Key Value Store Associations

```yaml
resource:
  aws_cloudfront_key_value_store:
    example:
      name: example-kvs
      comment: Example key value store

resource:
  aws_cloudfront_connection_function:
    example:
      name: example-connection-function
      connection_function_code: "function handler(event) { return event.request; }"
      connection_function_config:
        runtime: cloudfront-js-2.0
        comment: Example connection function
        key_value_store_association:
          key_value_store_arn: ${aws_cloudfront_key_value_store.example.arn}
```

## With Tags

```yaml
resource:
  aws_cloudfront_connection_function:
    example:
      name: example-connection-function
      connection_function_code: "function handler(event) { return event.request; }"
      connection_function_config:
        runtime: cloudfront-js-2.0
        comment: Example connection function
      tags:
        Environment: production
        Team: web
```

## Argument Reference

The following arguments are required:

* `connection_function_code` - (Required) Code for the connection function. Maximum length is 40960 characters.
* `connection_function_config` - (Required) Configuration information for the connection function. See [`connection_function_config`](#connection_function_config) below.
* `name` - (Required) Name for the connection function. Must be 1-64 characters and can contain letters, numbers, hyphens, and underscores. Changing this forces a new resource to be created.

The following arguments are optional:

* `key_value_store_associations` - (Optional) Configuration block for key value store associations. See [`key_value_store_associations`](#key_value_store_associations) below.
* `publish` - (Optional) Whether to publish the function to the `LIVE` stage after creation or update. Defaults to `false`.
* `tags` - (Optional) Map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### connection_function_config

* `comment` - (Required) Comment to describe the function.
* `key_value_store_association` - (Optional) Key value store associations. See [`key_value_store_association`](#key_value_store_association) below.
* `runtime` - (Required) Runtime environment for the function. Valid values are `cloudfront-js-1.0` and `cloudfront-js-2.0`.

### key_value_store_association

* `key_value_store_arn` - (Required) ARN of the key value store.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `connection_function_arn` - ARN of the connection function.
* `etag` - ETag of the connection function.
* `id` - ID of the connection function.
* `live_stage_etag` - ETag of the function's LIVE stage. Will be empty if the function has not been published.
* `status` - Status of the connection function.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_cloudfront_connection_function.example E1PA6795UKMFR9
```
