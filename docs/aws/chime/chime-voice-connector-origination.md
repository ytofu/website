# Chime Voice Connector Origination

Manage Chime Voice Connector Origination resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_chime_voice_connector:
    default:
      name: test
      require_encryption: true

resource:
  aws_chime_voice_connector_origination:
    default:
      disabled: false
      voice_connector_id: ${aws_chime_voice_connector.default.id}
      route:
        host: 127.0.0.1
        port: 8081
        protocol: TCP
        priority: 1
        weight: 1
      route:
        host: 127.0.0.2
        port: 8082
        protocol: TCP
        priority: 2
        weight: 10
```
