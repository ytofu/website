# Securitylake Subscriber

Manage Securitylake Subscriber resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_securitylake_subscriber:
    example:
      subscriber_name: example-name
      access_type: S3
      source:
        aws_log_source_resource:
          source_name: ROUTE53
          source_version: 1.0
      subscriber_identity:
        external_id: example
        principal: 1234567890
      depends_on: 
        - ${aws_securitylake_data_lake.example}
```

## Multiple Log Sources

```yaml
resource:
  aws_securitylake_subscriber:
    example:
      subscriber_name: example-name
      access_type: S3
      source:
        aws_log_source_resource:
          source_name: SH_FINDINGS
          source_version: 2.0
      source:
        aws_log_source_resource:
          source_name: ROUTE53
          source_version: 2.0
      subscriber_identity:
        external_id: example
        principal: 1234567890
      depends_on: 
        - ${aws_securitylake_data_lake.example}
```
