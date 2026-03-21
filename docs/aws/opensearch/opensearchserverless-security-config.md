# Opensearchserverless Security Config

Manage Opensearchserverless Security Config resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_opensearchserverless_security_config:
    example:
      name: example
      type: saml
      saml_options:
        metadata: file-content
```
