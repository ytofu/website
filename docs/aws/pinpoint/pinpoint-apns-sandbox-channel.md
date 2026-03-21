# Pinpoint Apns Sandbox Channel

Manage Pinpoint Apns Sandbox Channel resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_pinpoint_apns_sandbox_channel:
    apns_sandbox:
      application_id: ${aws_pinpoint_app.app.application_id}
      certificate: file-content
      private_key: file-content

resource:
  aws_pinpoint_app:
    app:
```
