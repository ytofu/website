# Resource: aws_spot_datafeed_subscription



## Basic Example

```yaml
resource:
  aws_s3_bucket:
    default:
      bucket: tf-spot-datafeed

  aws_spot_datafeed_subscription:
    default:
      bucket: ${aws_s3_bucket.default.id}
      prefix: my_subdirectory```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `bucket` - (Required) The Amazon S3 bucket in which to store the Spot instance data feed.
* `prefix` - (Optional) Path of folder inside bucket to place spot pricing data.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_spot_datafeed_subscription.mysubscription spot-datafeed-subscription
```
