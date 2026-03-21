# SES Receipt Rule

Manage SES Receipt Rule resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ses_receipt_rule:
    store:
      name: store
      rule_set_name: default-rule-set
      recipients: 
        - karen@example.com
      enabled: true
      scan_enabled: true
      add_header_action:
        header_name: Custom-Header
        header_value: Added by SES
        position: 1
      s3_action:
        bucket_name: emails
        position: 2
```
