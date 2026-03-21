# Opensearchserverless Access Policy

Manage Opensearchserverless Access Policy resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_opensearchserverless_access_policy:
    example:
      name: example
      type: data
      description: read and write permissions
      policy: 'example-json-policy'
```
