# Resource: aws_chimesdkvoice_global_settings

ytofu resource for managing Amazon Chime SDK Voice Global Settings.

## Basic Example

```yaml
resource:
  aws_chimesdkvoice_global_settings:
    example:
      voice_connector:
        cdr_bucket: example-bucket-name
```

## Argument Reference

This resource supports the following arguments:

* `voice_connector` - (Required) The Voice Connector settings. See [voice_connector](#voice_connector).

### `voice_connector`

The Amazon Chime SDK Voice Connector settings. Includes any Amazon S3 buckets designated for storing call detail records.

* `cdr_bucket` - (Optional) The S3 bucket that stores the Voice Connector's call detail records.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - AWS account ID for which the settings are applied.

## Import

```bash
ytofu import aws_chimesdkvoice_global_settings.example 123456789012
```
