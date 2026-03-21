# Resource: aws_cloudwatch_event_archive

Provides an EventBridge event archive resource.

## Basic Example

```yaml
resource:
  aws_cloudwatch_event_bus:
    order:
      name: orders

  aws_cloudwatch_event_archive:
    order:
      name: order-archive
      event_source_arn: ${aws_cloudwatch_event_bus.order.arn}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) Name of the archive. The archive name cannot exceed 48 characters.
* `event_source_arn` - (Required) ARN of the event bus associated with the archive. Only events from this event bus are sent to the archive.
* `description` - (Optional) Description for the archive.
* `event_pattern` - (Optional) Event pattern to use to filter events sent to the archive. By default, it attempts to archive every event received in the `event_source_arn`.
* `kms_key_identifier` - (Optional) Identifier of the AWS KMS customer managed key for EventBridge to use, if you choose to use a customer managed key to encrypt this archive. The identifier can be the key Amazon Resource Name (ARN), KeyId, key alias, or key alias ARN.
* `retention_days` - (Optional) The maximum number of days to retain events in the new event archive. By default, it archives indefinitely.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the archive.

## Import

```bash
ytofu import aws_cloudwatch_event_archive.imported_event_archive order-archive
```
