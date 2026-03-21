# Opensearchserverless Security Policy

Manage Opensearchserverless Security Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_opensearchserverless_security_policy:
    example:
      name: example
      type: encryption
      description: encryption security policy for example-collection
      policy: '{ "Rules": [ { "Resource": [ "collection/example-collection" ], "ResourceType": "collection" } ], "AWSOwnedKey": true }'
```

## Network Security Policy

```yaml
resource:
  aws_opensearchserverless_security_policy:
    example:
      name: example
      type: network
      description: Public access
      policy: 'example-json-policy'
```
