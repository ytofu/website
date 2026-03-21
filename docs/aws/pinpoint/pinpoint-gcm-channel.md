# Resource: aws_pinpoint_gcm_channel

Provides a Pinpoint GCM Channel resource.

## Basic Example

```yaml
resource:
  aws_pinpoint_gcm_channel:
    gcm:
      application_id: ${aws_pinpoint_app.app.application_id}
      default_authentication_method: TOKEN
      service_json: file-content

resource:
  aws_pinpoint_gcm_channel:
    gcm:
      application_id: ${aws_pinpoint_app.app.application_id}
      default_authentication_method: KEY
      api_key: api_key

resource:
  aws_pinpoint_app:
    app:
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `application_id` - (Required) The application ID.
* `api_key` - (Required) Platform credential API key from Google.
* `enabled` - (Optional) Whether the channel is enabled or disabled. Defaults to `true`.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_pinpoint_gcm_channel.gcm application-id
```
