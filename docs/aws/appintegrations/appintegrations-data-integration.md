# Appintegrations Data Integration

Manage Appintegrations Data Integration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appintegrations_data_integration:
    example:
      name: example
      description: example
      kms_key: ${aws_kms_key.test.arn}
      source_uri: "Salesforce://AppFlow/example"
      schedule_config:
        first_execution_from: 1439788442681
        object: Account
        schedule_expression: rate(1 hour)
      tags: 
```
