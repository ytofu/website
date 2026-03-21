# Pinpoint Adm Channel

Manage Pinpoint Adm Channel resources using ytofu YAML.

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
