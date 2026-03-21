# Devopsguru Service Integration

Manage Devopsguru Service Integration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_devopsguru_service_integration:
    example:
      kms_server_side_encryption:
        opt_in_status: ENABLED
        type: AWS_OWNED_KMS_KEY
      logs_anomaly_detection:
        opt_in_status: ENABLED
      ops_center:
        opt_in_status: ENABLED
```

## Customer Managed KMS Key

```yaml
resource:
  aws_kms_key:
    example:

resource:
  aws_devopsguru_service_integration:
    example:
      kms_server_side_encryption:
        kms_key_id: ${aws_kms_key.test.arn}
        opt_in_status: ENABLED
        type: CUSTOMER_MANAGED_KEY
      logs_anomaly_detection:
        opt_in_status: DISABLED
      ops_center:
        opt_in_status: DISABLED
```
