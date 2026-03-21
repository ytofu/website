# Cloudfront Connection Function

Manage Cloudfront Connection Function resources using ytofu YAML.

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
