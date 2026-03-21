# Cloudfront Monitoring Subscription

Manage Cloudfront Monitoring Subscription resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudfront_monitoring_subscription:
    example:
      distribution_id: ${aws_cloudfront_distribution.example.id}
      monitoring_subscription:
        realtime_metrics_subscription_config:
          realtime_metrics_subscription_status: Enabled
```
