# Resource: aws_shield_subscription

ytofu resource for managing an AWS Shield Subscription.

## Basic Example

```yaml
resource:
  aws_shield_subscription:
    example:
      auto_renew: ENABLED
```

## Argument Reference

The following arguments are optional:

* `auto_renew` - (Optional) Toggle for automated renewal of the subscription. Valid values are `ENABLED` or `DISABLED`. Default is `ENABLED`.
* `skip_destroy` - (Optional) Skip attempting to disable automated renewal upon destruction. If set to `true`, the `auto_renew` value will be left as-is and the resource will simply be removed from state.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - AWS Account ID.

## Import

```bash
ytofu import aws_shield_subscription.example 123456789012
```
