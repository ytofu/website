# Chimesdkvoice Sip Rule

Manage Chimesdkvoice Sip Rule resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_chimesdkvoice_sip_rule:
    example:
      name: example-sip-rule
      trigger_type: RequestUriHostname
      trigger_value: ${aws_chime_voice_connector.example-voice-connector.outbound_host_name}
      target_applications:
        priority: 1
        sip_media_application_id: ${aws_chimesdkvoice_sip_media_application.example-sma.id}
        aws_region: us-east-1
```
