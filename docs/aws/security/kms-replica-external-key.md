# KMS Replica External Key

Manage KMS Replica External Key resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_kms_external_key:
    primary:
      description: Multi-Region primary key
      deletion_window_in_days: 30
      multi_region: true
      enabled: true
      key_material_base64: ...

resource:
  aws_kms_replica_external_key:
    replica:
      description: Multi-Region replica key
      deletion_window_in_days: 7
      primary_key_arn: ${aws_kms_external_key.primary.arn}
      key_material_base64: "..." # Must be the same key material as the primary's.
```
