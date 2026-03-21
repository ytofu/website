# Spot Datafeed Subscription

Manage Spot Datafeed Subscription resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    default:
      bucket: tf-spot-datafeed

resource:
  aws_spot_datafeed_subscription:
    default:
      bucket: ${aws_s3_bucket.default.id}
      prefix: my_subdirectory
```
