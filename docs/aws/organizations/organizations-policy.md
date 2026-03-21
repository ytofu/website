# Organizations Policy

Manage Organizations Policy resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_iam_policy_document:
    example:
      statement:
        effect: Allow
        actions: 
          - "*"
        resources: 
          - "*"

resource:
  aws_organizations_policy:
    example:
      name: example
      content: ${data.aws_iam_policy_document.example.json}
```
