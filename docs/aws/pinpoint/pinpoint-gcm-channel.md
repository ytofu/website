# Pinpoint Gcm Channel

Manage Pinpoint Gcm Channel resources using ytofu YAML.

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
