# Transfer Host Key

Manage Transfer Host Key resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_transfer_host_key:
    example:
      server_id: ${aws_transfer_server.example.id}
      description: example additional host key
      host_key_body_wo: |
        # Private key PEM.
```
