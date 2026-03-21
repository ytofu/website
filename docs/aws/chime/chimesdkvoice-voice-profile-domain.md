# Chimesdkvoice Voice Profile Domain

Manage Chimesdkvoice Voice Profile Domain resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_kms_key:
    example:
      description: KMS Key for Voice Profile Domain
      deletion_window_in_days: 7

resource:
  aws_chimesdkvoice_voice_profile_domain:
    example:
      name: ExampleVoiceProfileDomain
      server_side_encryption_configuration:
        kms_key_arn: ${aws_kms_key.example.arn}
      description: My Voice Profile Domain
      tags:
        key1: value1
```
