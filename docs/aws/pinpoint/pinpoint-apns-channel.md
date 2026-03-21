# Pinpoint Apns Channel

Manage Pinpoint Apns Channel resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_pinpoint_apns_channel:
    apns:
      application_id: ${aws_pinpoint_app.app.application_id}
      certificate: file-content
      private_key: file-content

resource:
  aws_pinpoint_app:
    app:
```
