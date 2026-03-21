# Dynamodb Resource Policy

Manage Dynamodb Resource Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_dynamodb_resource_policy:
    example:
      resource_arn: ${aws_dynamodb_table.example.arn}
      policy: ${data.aws_iam_policy_document.test.json}
```
