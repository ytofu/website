# Pinpoint Sms Channel

Manage Pinpoint Sms Channel resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_pinpoint_sms_channel:
    sms:
      application_id: ${aws_pinpoint_app.app.application_id}

resource:
  aws_pinpoint_app:
    app:
```
