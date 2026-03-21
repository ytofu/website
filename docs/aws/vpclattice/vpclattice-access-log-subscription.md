# Vpclattice Access Log Subscription

Manage Vpclattice Access Log Subscription resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpclattice_access_log_subscription:
    example:
      resource_identifier: ${aws_vpclattice_service_network.example.id}
      destination_arn: ${aws_s3.bucket.arn}
```
