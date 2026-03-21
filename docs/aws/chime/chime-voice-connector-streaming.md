# Chime Voice Connector Streaming

Manage Chime Voice Connector Streaming resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_chime_voice_connector:
    default:
      name: vc-name-test
      require_encryption: true

resource:
  aws_chime_voice_connector_streaming:
    default:
      disabled: false
      voice_connector_id: ${aws_chime_voice_connector.default.id}
      data_retention: 7
      streaming_notification_targets: 
        - SQS
```

## Example Usage With Media Insights

```yaml
resource:
  aws_chime_voice_connector:
    default:
      name: vc-name-test
      require_encryption: true

resource:
  aws_chime_voice_connector_streaming:
    default:
      disabled: false
      voice_connector_id: ${aws_chime_voice_connector.default.id}
      data_retention: 7
      streaming_notification_targets: 
        - SQS
      media_insights_configuration:
        disabled: false
        configuration_arn: ${aws_chimesdkmediapipelines_media_insights_pipeline_configuration.example.arn}

resource:
  aws_chimesdkmediapipelines_media_insights_pipeline_configuration:
    example:
      name: ExampleConfig
      resource_access_role_arn: ${aws_iam_role.example.arn}
      elements:
        type: AmazonTranscribeCallAnalyticsProcessor
        amazon_transcribe_call_analytics_processor_configuration:
          language_code: en-US
      elements:
        type: KinesisDataStreamSink
        kinesis_data_stream_sink_configuration:
          insights_target: ${aws_kinesis_stream.example.arn}

data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - mediapipelines.chime.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    example:
      name: ExampleResourceAccessRole
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

resource:
  aws_kinesis_stream:
    example:
      name: ExampleStream
      shard_count: 2
```
