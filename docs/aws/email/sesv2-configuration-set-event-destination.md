# Sesv2 Configuration Set Event Destination

Manage Sesv2 Configuration Set Event Destination resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sesv2_configuration_set:
    example:
      configuration_set_name: example

resource:
  aws_sesv2_configuration_set_event_destination:
    example:
      configuration_set_name: ${aws_sesv2_configuration_set.example.configuration_set_name}
      event_destination_name: example
      event_destination:
        cloud_watch_destination:
          dimension_configuration:
            default_dimension_value: example
            dimension_name: example
            dimension_value_source: MESSAGE_TAG
        enabled: true
        matching_event_types: 
          - SEND
```

## EventBridge Destination

```yaml
data:
  aws_cloudwatch_event_bus:
    default:
      name: default

resource:
  aws_sesv2_configuration_set_event_destination:
    example:
      configuration_set_name: ${aws_sesv2_configuration_set.example.configuration_set_name}
      event_destination_name: example
      event_destination:
        event_bridge_destination:
          event_bus_arn: ${data.aws_cloudwatch_event_bus.default.arn}
        enabled: true
        matching_event_types: 
          - SEND
```

## Kinesis Firehose Destination

```yaml
resource:
  aws_sesv2_configuration_set:
    example:
      configuration_set_name: example

resource:
  aws_sesv2_configuration_set_event_destination:
    example:
      configuration_set_name: ${aws_sesv2_configuration_set.example.configuration_set_name}
      event_destination_name: example
      event_destination:
        kinesis_firehose_destination:
          delivery_stream_arn: ${aws_kinesis_firehose_delivery_stream.example.arn}
          iam_role_arn: ${aws_iam_role.example.arn}
        enabled: true
        matching_event_types: 
          - SEND
```

## Pinpoint Destination

```yaml
resource:
  aws_sesv2_configuration_set:
    example:
      configuration_set_name: example

resource:
  aws_sesv2_configuration_set_event_destination:
    example:
      configuration_set_name: ${aws_sesv2_configuration_set.example.configuration_set_name}
      event_destination_name: example
      event_destination:
        pinpoint_destination:
          application_arn: ${aws_pinpoint_app.example.arn}
        enabled: true
        matching_event_types: 
          - SEND
```

## SNS Destination

```yaml
resource:
  aws_sesv2_configuration_set:
    example:
      configuration_set_name: example

resource:
  aws_sesv2_configuration_set_event_destination:
    example:
      configuration_set_name: ${aws_sesv2_configuration_set.example.configuration_set_name}
      event_destination_name: example
      event_destination:
        sns_destination:
          topic_arn: ${aws_sns_topic.example.arn}
        enabled: true
        matching_event_types: 
          - SEND
```
