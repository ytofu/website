# Resource: aws_pinpoint_adm_channel

Provides a Pinpoint ADM (Amazon Device Messaging) Channel resource.

## Basic Example

```yaml
resource:
  aws_pinpoint_app:
    app:

resource:
  aws_pinpoint_adm_channel:
    channel:
      application_id: ${aws_pinpoint_app.app.application_id}
      client_id: 
      client_secret: 
      enabled: true
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `application_id` - (Required) The application ID.
* `client_id` - (Required) Client ID (part of OAuth Credentials) obtained via Amazon Developer Account.
* `client_secret` - (Required) Client Secret (part of OAuth Credentials) obtained via Amazon Developer Account.
* `enabled` - (Optional) Specifies whether to enable the channel. Defaults to `true`.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_pinpoint_adm_channel.channel application-id
```
