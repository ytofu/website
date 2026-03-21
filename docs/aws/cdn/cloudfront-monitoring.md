# CloudFront Monitoring Subscription

Enable additional metrics for CloudFront distributions using ytofu YAML.

## Enable Monitoring

```yaml
resource:
  aws_cloudfront_monitoring_subscription:
    example:
      distribution_id: ${aws_cloudfront_distribution.example.id}
      monitoring_subscription:
        realtime_metrics_subscription_config:
          realtime_metrics_subscription_status: Enabled
```
