# Verifiedaccess Group

Manage Verifiedaccess Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_verifiedaccess_group:
    example:
      verifiedaccess_instance_id: ${aws_verifiedaccess_instance.example.id}
```

## Usage with KMS Key

```yaml
resource:
  aws_kms_key:
    test_key:
      description: KMS key for Verified Access Group test

resource:
  aws_verifiedaccess_group:
    test:
      verifiedaccess_instance_id: ${aws_verifiedaccess_instance_trust_provider_attachment.test.verifiedaccess_instance_id}
      sse_configuration:
        kms_key_arn: ${aws_kms_key.test_key.arn}
```
