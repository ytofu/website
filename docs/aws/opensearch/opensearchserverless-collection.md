# Opensearchserverless Collection

Manage Opensearchserverless Collection resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_opensearchserverless_security_policy:
    example:
      name: example
      type: encryption
      policy: '{ "Rules" = [ { "Resource" = [ "collection/example" ], "ResourceType" = "collection" } ], "AWSOwnedKey" = true }'

resource:
  aws_opensearchserverless_collection:
    example:
      name: example
      depends_on: 
        - ${aws_opensearchserverless_security_policy.example}
```
