# Resource: aws_pinpoint_sms_channel

Use the `aws_pinpoint_sms_channel` resource to manage Pinpoint SMS Channels.

## Basic Example

```yaml
resource:
  aws_pinpoint_sms_channel:
    sms:
      application_id: ${aws_pinpoint_app.app.application_id}

  aws_pinpoint_app:
    app:```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `application_id` - (Required) ID of the application.
* `enabled` - (Optional) Whether the channel is enabled or disabled. By default, it is set to `true`.
* `sender_id` - (Optional) Identifier of the sender for your messages.
* `short_code` - (Optional) Short Code registered with the phone provider.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `promotional_messages_per_second` - Maximum number of promotional messages that can be sent per second.
* `transactional_messages_per_second` - Maximum number of transactional messages per second that can be sent.

## Import

```bash
ytofu import aws_pinpoint_sms_channel.sms application-id
```
