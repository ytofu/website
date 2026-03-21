# Resource: aws_ec2_image_block_public_access

Provides a regional public access block for AMIs. This prevents AMIs from being made publicly accessible.
If you already have public AMIs, they will remain publicly available.

## Basic Example

```yaml
resource:
  aws_ec2_image_block_public_access:
    test:
      state: block-new-sharing
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `state` - (Required) The state of block public access for AMIs at the account level in the configured AWS Region. Valid values: `unblocked` and `block-new-sharing`.

## Attribute Reference

This resource exports no additional attributes.

## Timeouts

Configuration options:

- `update` - (Default `10m`)
