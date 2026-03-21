# Resource: aws_chime_voice_connector_group

Creates an Amazon Chime Voice Connector group under the administrator's AWS account. You can associate Amazon Chime Voice Connectors with the Amazon Chime Voice Connector group by including VoiceConnectorItems in the request.

## Basic Example

```yaml
resource:
  aws_chime_voice_connector:
    vc1:
      name: connector-test-1
      require_encryption: true
      aws_region: us-east-1

  aws_chime_voice_connector:
    vc2:
      name: connector-test-2
      require_encryption: true
      aws_region: us-west-2

  aws_chime_voice_connector_group:
    group:
      name: test-group
      connector:
        voice_connector_id: ${aws_chime_voice_connector.vc1.id}
        priority: 1
      connector:
        voice_connector_id: ${aws_chime_voice_connector.vc2.id}
        priority: 3```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the Amazon Chime Voice Connector group.
* `connector` - (Optional) The Amazon Chime Voice Connectors to route inbound calls to.

### `connector`

For Amazon Chime Voice Connector groups, the Amazon Chime Voice Connectors to which to route inbound calls. Includes priority configuration settings. Limit: 3 VoiceConnectorItems per Amazon Chime Voice Connector group.

* `voice_connector_id` - (Required) The Amazon Chime Voice Connector ID.
* `priority` - (Required) The priority associated with the Amazon Chime Voice Connector, with 1 being the highest priority. Higher priority Amazon Chime Voice Connectors are attempted first.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Amazon Chime Voice Connector group ID.

## Import

```bash
ytofu import aws_chime_voice_connector_group.default example
```
