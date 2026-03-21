# Resource: aws_cloudfront_key_group

## Example Usage

## Basic Example

```yaml
resource:
  aws_cloudfront_public_key:
    example:
      comment: example public key
      encoded_key: file-content
      name: example-key

resource:
  aws_cloudfront_key_group:
    example:
      comment: example key group
      items: 
        - ${aws_cloudfront_public_key.example.id}
      name: example-key-group
```

## Argument Reference

This resource supports the following arguments:

* `comment` - (Optional) A comment to describe the key group..
* `items` - (Required) A list of the identifiers of the public keys in the key group.
* `name` - (Required) A name to identify the key group.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `etag` - The identifier for this version of the key group.
* `id` - The identifier for the key group.

## Import

```bash
ytofu import aws_cloudfront_key_group.example 4b4f2r1c-315d-5c2e-f093-216t50jed10f
```
