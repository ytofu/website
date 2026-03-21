# Chimesdkmediapipelines Media Insights Pipeline Configuration

Manage Chimesdkmediapipelines Media Insights Pipeline Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_chimesdkmediapipelines_media_insights_pipeline_configuration:
    my_configuration:
      name: MyBasicConfiguration
      resource_access_role_arn: ${aws_iam_role.call_analytics_role.arn}
      elements:
        type: AmazonTranscribeCallAnalyticsProcessor
        amazon_transcribe_call_analytics_processor_configuration:
          language_code: en-US
      elements:
        type: KinesisDataStreamSink
        kinesis_data_stream_sink_configuration:
          insights_target: ${aws_kinesis_stream.example.arn}
      tags:
        Key1: Value1
        Key2: Value2

resource:
  aws_kinesis_stream:
    example:
      name: example
      shard_count: 2

data:
  aws_iam_policy_document:
    media_pipelines_assume_role:
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
    call_analytics_role:
      name: CallAnalyticsRole
      assume_role_policy: ${data.aws_iam_policy_document.media_pipelines_assume_role.json}
```

## Transcribe Call Analytics processor usage

```yaml
resource:
  aws_chimesdkmediapipelines_media_insights_pipeline_configuration:
    my_configuration:
      name: MyCallAnalyticsConfiguration
      resource_access_role_arn: ${aws_iam_role.example.arn}
      elements:
        type: AmazonTranscribeCallAnalyticsProcessor
        amazon_transcribe_call_analytics_processor_configuration:
          call_analytics_stream_categories:
            - category_1
            - category_2
          content_redaction_type: PII
          enable_partial_results_stabilization: true
          filter_partial_results: true
          language_code: en-US
          language_model_name: MyLanguageModel
          partial_results_stability: high
          pii_entity_types: ADDRESS,BANK_ACCOUNT_NUMBER
          post_call_analytics_settings:
            content_redaction_output: redacted
            data_access_role_arn: ${aws_iam_role.post_call_role.arn}
            output_encryption_kms_key_id: MyKmsKeyId
            output_location: "s3://MyBucket"
          vocabulary_filter_method: mask
          vocabulary_filter_name: MyVocabularyFilter
          vocabulary_name: MyVocabulary
      elements:
        type: KinesisDataStreamSink
        kinesis_data_stream_sink_configuration:
          insights_target: ${aws_kinesis_stream.example.arn}

data:
  aws_iam_policy_document:
    transcribe_assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - transcribe.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    post_call_role:
      name: PostCallAccessRole
      assume_role_policy: ${data.aws_iam_policy_document.transcribe_assume_role.json}
```

## Real time alerts usage

```yaml
resource:
  aws_chimesdkmediapipelines_media_insights_pipeline_configuration:
    my_configuration:
      name: MyRealTimeAlertConfiguration
      resource_access_role_arn: ${aws_iam_role.call_analytics_role.arn}
      elements:
        type: AmazonTranscribeCallAnalyticsProcessor
        amazon_transcribe_call_analytics_processor_configuration:
          language_code: en-US
      elements:
        type: KinesisDataStreamSink
        kinesis_data_stream_sink_configuration:
          insights_target: ${aws_kinesis_stream.example.arn}
      real_time_alert_configuration:
        disabled: false
        rules:
          type: IssueDetection
          issue_detection_configuration:
            rule_name: MyIssueDetectionRule
        rules:
          type: KeywordMatch
          keyword_match_configuration:
            keywords: 
              - keyword1
              - keyword2
            negate: false
            rule_name: MyKeywordMatchRule
        rules:
          type: Sentiment
          sentiment_configuration:
            rule_name: MySentimentRule
            sentiment_type: NEGATIVE
            time_period: 60
```

## Transcribe processor usage

```yaml
resource:
  aws_chimesdkmediapipelines_media_insights_pipeline_configuration:
    my_configuration:
      name: MyTranscribeConfiguration
      resource_access_role_arn: ${aws_iam_role.example.arn}
      elements:
        type: AmazonTranscribeProcessor
        amazon_transcribe_processor_configuration:
          content_identification_type: PII
          enable_partial_results_stabilization: true
          filter_partial_results: true
          language_code: en-US
          language_model_name: MyLanguageModel
          partial_results_stability: high
          pii_entity_types: ADDRESS,BANK_ACCOUNT_NUMBER
          show_speaker_label: true
          vocabulary_filter_method: mask
          vocabulary_filter_name: MyVocabularyFilter
          vocabulary_name: MyVocabulary
      elements:
        type: KinesisDataStreamSink
        kinesis_data_stream_sink_configuration:
          insights_target: ${aws_kinesis_stream.example.arn}
```

## Voice analytics processor usage

```yaml
resource:
  aws_chimesdkmediapipelines_media_insights_pipeline_configuration:
    my_configuration:
      name: MyVoiceAnalyticsConfiguration
      resource_access_role_arn: ${aws_iam_role.example.arn}
      elements:
        type: VoiceAnalyticsProcessor
        voice_analytics_processor_configuration:
          speaker_search_status: Enabled
          voice_tone_analysis_status: Enabled
      elements:
        type: LambdaFunctionSink
        lambda_function_sink_configuration:
          insights_target: "arn:aws:lambda:us-west-2:1111111111:function:MyFunction"
      elements:
        type: SnsTopicSink
        sns_topic_sink_configuration:
          insights_target: "arn:aws:sns:us-west-2:1111111111:topic/MyTopic"
      elements:
        type: SqsQueueSink
        sqs_queue_sink_configuration:
          insights_target: "arn:aws:sqs:us-west-2:1111111111:queue/MyQueue"
      elements:
        type: KinesisDataStreamSink
        kinesis_data_stream_sink_configuration:
          insights_target: ${aws_kinesis_stream.test.arn}
```

## S3 Recording sink usage

```yaml
resource:
  aws_chimesdkmediapipelines_media_insights_pipeline_configuration:
    my_configuration:
      name: MyS3RecordingConfiguration
      resource_access_role_arn: ${aws_iam_role.example.arn}
      elements:
        type: S3RecordingSink
        s3_recording_sink_configuration:
          destination: "arn:aws:s3:::MyBucket"
```
