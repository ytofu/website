# Cloudfront Field Level Encryption Profile

Manage Cloudfront Field Level Encryption Profile resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudfront_public_key:
    example:
      comment: test public key
      encoded_key: file-content
      name: test_key

resource:
  aws_cloudfront_field_level_encryption_profile:
    test:
      comment: test comment
      name: test profile
      encryption_entities:
        items:
          public_key_id: ${aws_cloudfront_public_key.example.id}
          provider_id: test provider
          field_patterns:
            items: 
              - DateOfBirth
```
