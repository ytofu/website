# Resource: aws_pinpoint_baidu_channel

Provides a Pinpoint Baidu Channel resource.

## Basic Example

```yaml
resource:
  aws_pinpoint_app:
    app:

resource:
  aws_pinpoint_baidu_channel:
    channel:
      application_id: ${aws_pinpoint_app.app.application_id}
      api_key: 
      secret_key: 
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `application_id` - (Required) The application ID.
* `enabled` - (Optional) Specifies whether to enable the channel. Defaults to `true`.
* `api_key` - (Required) Platform credential API key from Baidu.
* `secret_key` - (Required) Platform credential Secret key from Baidu.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_pinpoint_baidu_channel.channel application-id
```
