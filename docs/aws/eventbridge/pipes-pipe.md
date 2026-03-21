# Pipes Pipe

Manage Pipes Pipe resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    main:

resource:
  aws_iam_role:
    example:
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": { "Effect": "Allow" "Action": "sts:AssumeRole" "Principal": { "Service": "pipes.amazonaws.com" } "Condition": { "StringEquals": { "aws:SourceAccount" = data.aws_caller_identity.main.account_id } } } }'

resource:
  aws_iam_role_policy:
    source:
      role: ${aws_iam_role.example.id}
      policy: '{ "Version": "2012-10-17" "Statement": [ { "Effect": "Allow" "Action": [ "sqs:DeleteMessage", "sqs:GetQueueAttributes", "sqs:ReceiveMessage", ], "Resource": [ aws_sqs_queue.source.arn, ] }, ] }'

resource:
  aws_sqs_queue:
    source:

resource:
  aws_iam_role_policy:
    target:
      role: ${aws_iam_role.example.id}
      policy: '{ "Version": "2012-10-17" "Statement": [ { "Effect": "Allow" "Action": [ "sqs:SendMessage", ], "Resource": [ aws_sqs_queue.target.arn, ] }, ] }'

resource:
  aws_sqs_queue:
    target:

resource:
  aws_pipes_pipe:
    example:
      depends_on: 
        - ${aws_iam_role_policy.source}
        - ${aws_iam_role_policy.target}
      name: example-pipe
      role_arn: ${aws_iam_role.example.arn}
      source: ${aws_sqs_queue.source.arn}
      target: ${aws_sqs_queue.target.arn}
```

## Enrichment Usage

```yaml
resource:
  aws_pipes_pipe:
    example:
      name: example-pipe
      role_arn: ${aws_iam_role.example.arn}
      source: ${aws_sqs_queue.source.arn}
      target: ${aws_sqs_queue.target.arn}
      enrichment: ${aws_cloudwatch_event_api_destination.example.arn}
      enrichment_parameters:
        http_parameters:
          path_parameter_values: 
            - example-path-param
          header_parameters: 
          query_string_parameters: 
```

## Filter Usage

```yaml
resource:
  aws_pipes_pipe:
    example:
      name: example-pipe
      role_arn: ${aws_iam_role.example.arn}
      source: ${aws_sqs_queue.source.arn}
      target: ${aws_sqs_queue.target.arn}
      source_parameters:
        filter_criteria:
          filter:
            pattern: '{ "source": ["event-source"] }'
```

## CloudWatch Logs Logging Configuration Usage

```yaml
resource:
  aws_cloudwatch_log_group:
    example:
      name: example-pipe-target

resource:
  aws_pipes_pipe:
    example:
      depends_on: 
        - ${aws_iam_role_policy.source}
        - ${aws_iam_role_policy.target}
      name: example-pipe
      role_arn: ${aws_iam_role.example.arn}
      source: ${aws_sqs_queue.source.arn}
      target: ${aws_sqs_queue.target.arn}
      log_configuration:
        include_execution_data: 
          - ALL
        level: INFO
        cloudwatch_logs_log_destination:
          log_group_arn: ${aws_cloudwatch_log_group.target.arn}
```

## SQS Source and Target Configuration Usage

```yaml
resource:
  aws_pipes_pipe:
    example:
      name: example-pipe
      role_arn: ${aws_iam_role.example.arn}
      source: ${aws_sqs_queue.source.arn}
      target: ${aws_sqs_queue.target.arn}
      source_parameters:
        sqs_queue_parameters:
          batch_size: 1
          maximum_batching_window_in_seconds: 2
      target_parameters:
        sqs_queue_parameters:
          message_deduplication_id: example-dedupe
          message_group_id: example-group
```
