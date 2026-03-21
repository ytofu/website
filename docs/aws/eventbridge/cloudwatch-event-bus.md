# Cloudwatch Event Bus

Manage Cloudwatch Event Bus resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudwatch_event_bus:
    messenger:
      name: chat-messages
```

## Logging to CloudWatch Logs, S3, and Data Firehose

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_cloudwatch_event_bus:
    example:
      name: example-event-bus
      log_config:
        include_detail: FULL
        level: TRACE

resource:
  aws_cloudwatch_log_delivery_source:
    info_logs:
      name: "EventBusSource-${aws_cloudwatch_event_bus.example.name}-INFO_LOGS"
      log_type: INFO_LOGS
      resource_arn: ${aws_cloudwatch_event_bus.example.arn}

resource:
  aws_cloudwatch_log_delivery_source:
    error_logs:
      name: "EventBusSource-${aws_cloudwatch_event_bus.example.name}-ERROR_LOGS"
      log_type: ERROR_LOGS
      resource_arn: ${aws_cloudwatch_event_bus.example.arn}

resource:
  aws_cloudwatch_log_delivery_source:
    trace_logs:
      name: "EventBusSource-${aws_cloudwatch_event_bus.example.name}-TRACE_LOGS"
      log_type: TRACE_LOGS
      resource_arn: ${aws_cloudwatch_event_bus.example.arn}

resource:
  aws_s3_bucket:
    example:
      bucket: example-event-bus-logs

data:
  aws_iam_policy_document:
    bucket:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - delivery.logs.amazonaws.com
        actions:
          - "s3:PutObject"
        resources:
          - "${aws_s3_bucket.example.arn}/AWSLogs/${data.aws_caller_identity.current.account_id}/EventBusLogs/*"
        condition:
          test: StringEquals
          values: 
            - bucket-owner-full-control
        condition:
          test: StringEquals
          values: 
            - ${data.aws_caller_identity.current.account_id}
        condition:
          test: ArnLike
          values:
            - ${aws_cloudwatch_log_delivery_source.info_logs.arn}
            - ${aws_cloudwatch_log_delivery_source.error_logs.arn}
            - ${aws_cloudwatch_log_delivery_source.trace_logs.arn}

resource:
  aws_s3_bucket_policy:
    example:
      bucket: ${aws_s3_bucket.example.bucket}
      policy: ${data.aws_iam_policy_document.bucket.json}

resource:
  aws_cloudwatch_log_delivery_destination:
    s3:
      name: "EventsDeliveryDestination-${aws_cloudwatch_event_bus.example.name}-S3"
      delivery_destination_configuration:
        destination_resource_arn: ${aws_s3_bucket.example.arn}

resource:
  aws_cloudwatch_log_delivery:
    s3_info_logs:
      delivery_destination_arn: ${aws_cloudwatch_log_delivery_destination.s3.arn}
      delivery_source_name: ${aws_cloudwatch_log_delivery_source.info_logs.name}

resource:
  aws_cloudwatch_log_delivery:
    s3_error_logs:
      delivery_destination_arn: ${aws_cloudwatch_log_delivery_destination.s3.arn}
      delivery_source_name: ${aws_cloudwatch_log_delivery_source.error_logs.name}
      depends_on:
        - ${aws_cloudwatch_log_delivery.s3_info_logs}

resource:
  aws_cloudwatch_log_delivery:
    s3_trace_logs:
      delivery_destination_arn: ${aws_cloudwatch_log_delivery_destination.s3.arn}
      delivery_source_name: ${aws_cloudwatch_log_delivery_source.trace_logs.name}
      depends_on:
        - ${aws_cloudwatch_log_delivery.s3_error_logs}

resource:
  aws_cloudwatch_log_group:
    event_bus_logs:
      name: "/aws/vendedlogs/events/event-bus/${aws_cloudwatch_event_bus.example.name}"

data:
  aws_iam_policy_document:
    cwlogs:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - delivery.logs.amazonaws.com
        actions:
          - "logs:CreateLogStream"
          - "logs:PutLogEvents"
        resources:
          - "${aws_cloudwatch_log_group.event_bus_logs.arn}:log-stream:*"
        condition:
          test: StringEquals
          values: 
            - ${data.aws_caller_identity.current.account_id}
        condition:
          test: ArnLike
          values:
            - ${aws_cloudwatch_log_delivery_source.info_logs.arn}
            - ${aws_cloudwatch_log_delivery_source.error_logs.arn}
            - ${aws_cloudwatch_log_delivery_source.trace_logs.arn}

resource:
  aws_cloudwatch_log_resource_policy:
    example:
      policy_document: ${data.aws_iam_policy_document.cwlogs.json}
      policy_name: "AWSLogDeliveryWrite-${aws_cloudwatch_event_bus.example.name}"

resource:
  aws_cloudwatch_log_delivery_destination:
    cwlogs:
      name: "EventsDeliveryDestination-${aws_cloudwatch_event_bus.example.name}-CWLogs"
      delivery_destination_configuration:
        destination_resource_arn: ${aws_cloudwatch_log_group.event_bus_logs.arn}

resource:
  aws_cloudwatch_log_delivery:
    cwlogs_info_logs:
      delivery_destination_arn: ${aws_cloudwatch_log_delivery_destination.cwlogs.arn}
      delivery_source_name: ${aws_cloudwatch_log_delivery_source.info_logs.name}
      depends_on:
        - ${aws_cloudwatch_log_delivery.s3_info_logs}

resource:
  aws_cloudwatch_log_delivery:
    cwlogs_error_logs:
      delivery_destination_arn: ${aws_cloudwatch_log_delivery_destination.cwlogs.arn}
      delivery_source_name: ${aws_cloudwatch_log_delivery_source.error_logs.name}
      depends_on:
        - ${aws_cloudwatch_log_delivery.s3_error_logs}
        - ${aws_cloudwatch_log_delivery.cwlogs_info_logs}

resource:
  aws_cloudwatch_log_delivery:
    cwlogs_trace_logs:
      delivery_destination_arn: ${aws_cloudwatch_log_delivery_destination.cwlogs.arn}
      delivery_source_name: ${aws_cloudwatch_log_delivery_source.trace_logs.name}
      depends_on:
        - ${aws_cloudwatch_log_delivery.s3_trace_logs}
        - ${aws_cloudwatch_log_delivery.cwlogs_error_logs}

resource:
  aws_kinesis_firehose_delivery_stream:
    cloudfront_logs:
      tags:
        LogDeliveryEnabled: true

resource:
  aws_cloudwatch_log_delivery_destination:
    firehose:
      name: "EventsDeliveryDestination-${aws_cloudwatch_event_bus.example.name}-Firehose"
      delivery_destination_configuration:
        destination_resource_arn: ${aws_kinesis_firehose_delivery_stream.cloudfront_logs.arn}

resource:
  aws_cloudwatch_log_delivery:
    firehose_info_logs:
      delivery_destination_arn: ${aws_cloudwatch_log_delivery_destination.firehose.arn}
      delivery_source_name: ${aws_cloudwatch_log_delivery_source.info_logs.name}
      depends_on:
        - ${aws_cloudwatch_log_delivery.cwlogs_info_logs}

resource:
  aws_cloudwatch_log_delivery:
    firehose_error_logs:
      delivery_destination_arn: ${aws_cloudwatch_log_delivery_destination.firehose.arn}
      delivery_source_name: ${aws_cloudwatch_log_delivery_source.error_logs.name}
      depends_on:
        - ${aws_cloudwatch_log_delivery.cwlogs_error_logs}
        - ${aws_cloudwatch_log_delivery.firehose_info_logs}

resource:
  aws_cloudwatch_log_delivery:
    firehose_trace_logs:
      delivery_destination_arn: ${aws_cloudwatch_log_delivery_destination.firehose.arn}
      delivery_source_name: ${aws_cloudwatch_log_delivery_source.trace_logs.name}
      depends_on:
        - ${aws_cloudwatch_log_delivery.cwlogs_trace_logs}
        - ${aws_cloudwatch_log_delivery.firehose_error_logs}
```
