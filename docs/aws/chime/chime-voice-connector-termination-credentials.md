# Resource: aws_chime_voice_connector_termination_credentials

Adds termination SIP credentials for the specified Amazon Chime Voice Connector.

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `voice_connector_id` - (Required) Amazon Chime Voice Connector ID.
* `credentials` - (Required) List of termination SIP credentials.

### `credentials`

The SIP credentials used to authenticate requests to your Amazon Chime Voice Connector.

* `username` - (Required) RFC2617 compliant username associated with the SIP credentials.
* `password` - (Required) RFC2617 compliant password associated with the SIP credentials.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Amazon Chime Voice Connector ID.

## Import

```bash
ytofu import aws_chime_voice_connector_termination_credentials.default abcdef1ghij2klmno3pqr4
```
