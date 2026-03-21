# Securitylake Custom Log Source

Manage Securitylake Custom Log Source resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_securitylake_custom_log_source:
    example:
      source_name: example-name
      source_version: 1.0
      event_classes: 
        - FILE_ACTIVITY
      configuration:
        crawler_configuration:
          role_arn: ${aws_iam_role.custom_log.arn}
        provider_identity:
          external_id: example-id
          principal: 123456789012
      depends_on: 
        - ${aws_securitylake_data_lake.example}
```
