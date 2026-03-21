# AWS Config Remediation

Configure automatic remediation for non-compliant resources using ytofu YAML.

## Basic Remediation

```yaml
resource:
  aws_config_remediation_configuration:
    example:
      config_rule_name: ${aws_config_config_rule.example.name}
      target_type: SSM_DOCUMENT
      target_id: AWS-EnableS3BucketEncryption
      automatic: true
      maximum_automatic_attempts: 3
      retry_attempt_seconds: 60
```
