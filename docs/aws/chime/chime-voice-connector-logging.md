# Resource: aws_chime_voice_connector_logging

Adds a logging configuration for the specified Amazon Chime Voice Connector. The logging configuration specifies whether SIP message logs are enabled for sending to Amazon CloudWatch Logs.

## Basic Example

```yaml
resource:
  aws_chime_voice_connector:
    default:
      name: vc-name-test
      require_encryption: true

  aws_chime_voice_connector_logging:
    default:
      enable_sip_logs: true
      enable_media_metric_logs: true
      voice_connector_id: ${aws_chime_voice_connector.default.id}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `voice_connector_id` - (Required) The Amazon Chime Voice Connector ID.
* `enable_sip_logs` - (Optional) When true, enables SIP message logs for sending to Amazon CloudWatch Logs.
* `enable_media_metric_logs` - (Optional) When true, enables logging of detailed media metrics for Voice Connectors to Amazon CloudWatch logs.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The Amazon Chime Voice Connector ID.

## Import

```bash
ytofu import aws_chime_voice_connector_logging.default abcdef1ghij2klmno3pqr4
```
