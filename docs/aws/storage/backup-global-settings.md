# Resource: aws_backup_global_settings

Provides an AWS Backup Global Settings resource.

## Basic Example

```yaml
resource:
  aws_backup_global_settings:
    test:
      global_settings: 
```

## Argument Reference

This resource supports the following arguments:

* `global_settings` - (Required) A list of resources along with the opt-in preferences for the account. For a list of inputs, see [UpdateGlobalSettings](https://docs.aws.amazon.com/aws-backup/latest/devguide/API_UpdateGlobalSettings.html) in the AWS Backup Developer Guide.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The AWS Account ID.

## Import

```bash
ytofu import aws_backup_global_settings.example 123456789012
```
