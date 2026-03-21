# Chime Voice Connector Termination Credentials

Manage Chime Voice Connector Termination Credentials resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_chime_voice_connector:
    default:
      name: test
      require_encryption: true

resource:
  aws_chime_voice_connector_termination:
    default:
      disabled: true
      cps_limit: 1
      cidr_allow_list: 
        - 50.35.78.96/31
      calling_regions: 
        - US
        - CA
      voice_connector_id: ${aws_chime_voice_connector.default.id}

resource:
  aws_chime_voice_connector_termination_credentials:
    default:
      voice_connector_id: ${aws_chime_voice_connector.default.id}
      credentials:
        username: test
        password: test!
      depends_on: 
        - ${aws_chime_voice_connector_termination.default}
```
