# Transfer Profile

Manage Transfer Profile resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_transfer_profile:
    example:
      as2_id: example
      certificate_ids: 
        - ${aws_transfer_certificate.example.certificate_id}
      usage: LOCAL
```
