# Chime Voice Connector Termination

Manage Chime Voice Connector Termination resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_chime_voice_connector:
    default:
      name: vc-name-test
      require_encryption: true

resource:
  aws_chime_voice_connector_termination:
    default:
      disabled: false
      cps_limit: 1
      cidr_allow_list: 
        - 50.35.78.96/31
      calling_regions: 
        - US
        - CA
      voice_connector_id: ${aws_chime_voice_connector.default.id}
```
