# Resource: aws_waf_byte_match_set

Provides a WAF Byte Match Set Resource

## Basic Example

```yaml
resource:
  aws_waf_byte_match_set:
    byte_set:
      name: tf_waf_byte_match_set
      byte_match_tuples:
        text_transformation: NONE
        target_string: badrefer1
        positional_constraint: CONTAINS
        field_to_match:
          type: HEADER
          data: referer
```

## Argument Reference

This resource supports the following arguments:

* `name` - (Required) The name or description of the Byte Match Set.
* `byte_match_tuples` - Specifies the bytes (typically a string that corresponds
  with ASCII characters) that you want to search for in web requests,
  the location in requests that you want to search, and other settings.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the WAF Byte Match Set.
* `arn` - Amazon Resource Name (ARN) of the byte match set.

## Import

```bash
ytofu import aws_waf_byte_match_set.byte_set a1b2c3d4-d5f6-7777-8888-9999aaaabbbbcccc
```
