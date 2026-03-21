# Transfer Certificate

Manage Transfer Certificate resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_transfer_certificate:
    example:
      certificate: file-content
      certificate_chain: file-content
      private_key: file-content
      description: example
      usage: SIGNING
```
