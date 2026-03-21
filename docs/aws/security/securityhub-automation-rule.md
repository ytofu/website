# Securityhub Automation Rule

Manage Securityhub Automation Rule resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_securityhub_automation_rule:
    example:
      description: Elevate finding severity to CRITICAL when specific resources such as an S3 bucket is at risk
      rule_name: Elevate severity of findings that relate to important resources
      rule_order: 1
      actions:
        finding_fields_update:
          severity:
            label: CRITICAL
            product: 0.0
          note:
            text: This is a critical resource. Please review ASAP.
            updated_by: sechub-automation
          types: 
            - Software and Configuration Checks/Industry and Regulatory Standards
          user_defined_fields:
            key: value
        type: FINDING_FIELDS_UPDATE
      criteria:
        resource_id:
          comparison: EQUALS
          value: "arn:aws:s3:::examplebucket/*"
```
