# Resource: aws_chimesdkvoice_voice_profile_domain

ytofu resource for managing an AWS Chime SDK Voice Profile Domain.

## Basic Example

```yaml
resource:
  aws_kms_key:
    example:
      description: KMS Key for Voice Profile Domain
      deletion_window_in_days: 7

  aws_chimesdkvoice_voice_profile_domain:
    example:
      name: ExampleVoiceProfileDomain
      server_side_encryption_configuration:
        kms_key_arn: ${aws_kms_key.example.arn}
      description: My Voice Profile Domain
      tags:
        key1: value1```

## Argument Reference

The following arguments are required:

* `name` - (Required) Name of Voice Profile Domain.
* `server_side_encryption_configuration` - (Required) Configuration for server side encryption.
    * `kms_key_arn` - (Required) ARN for KMS Key.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) Description of Voice Profile Domain.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Voice Profile Domain.
* `id` - ID of the Voice Profile Domain.

## Timeouts

Configuration options:

* `create` - (Default `30s`)
* `update` - (Default `30s`)
* `delete` - (Default `30s`)

## Import

```bash
ytofu import aws_chimesdkvoice_voice_profile_domain.example abcdef123456
```
