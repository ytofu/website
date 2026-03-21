# Schemas Registry Policy

Manage Schemas Registry Policy resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_iam_policy_document:
    example:
      statement:
        sid: example
        effect: Allow
        principals:
          type: AWS
          identifiers:
            - 109876543210
        actions: 
          - "schemas:*"
        resources:
          - "arn:aws:schemas:us-east-1:123456789012:registry/example"
          - "arn:aws:schemas:us-east-1:123456789012:schema/example*"

resource:
  aws_schemas_registry_policy:
    example:
      registry_name: example
      policy: ${data.aws_iam_policy_document.example.json}
```
