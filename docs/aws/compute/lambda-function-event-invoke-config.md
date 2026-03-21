# Lambda Function Event Invoke Config

Manage Lambda Function Event Invoke Config resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sqs_queue:
    dlq:
      name: lambda-dlq
      tags:
        Environment: production
        Purpose: lambda-error-handling

resource:
  aws_sns_topic:
    success:
      name: lambda-success-notifications
      tags:
        Environment: production
        Purpose: lambda-success-notifications

resource:
  aws_lambda_function_event_invoke_config:
    example:
      function_name: ${aws_lambda_function.example.function_name}
      maximum_event_age_in_seconds: 300
      maximum_retry_attempts: 1
      destination_config:
        on_failure:
          destination: ${aws_sqs_queue.dlq.arn}
        on_success:
          destination: ${aws_sns_topic.success.arn}
```

## Error Handling Only

```yaml
resource:
  aws_lambda_function_event_invoke_config:
    example:
      function_name: ${aws_lambda_function.example.function_name}
      maximum_event_age_in_seconds: 60
      maximum_retry_attempts: 0
```

## Configuration for Lambda Alias

```yaml
resource:
  aws_lambda_alias:
    example:
      name: production
      description: Production alias
      function_name: ${aws_lambda_function.example.function_name}
      function_version: ${aws_lambda_function.example.version}

resource:
  aws_lambda_function_event_invoke_config:
    example:
      function_name: ${aws_lambda_function.example.function_name}
      qualifier: ${aws_lambda_alias.example.name}
      maximum_event_age_in_seconds: 1800
      maximum_retry_attempts: 2
      destination_config:
        on_failure:
          destination: ${aws_sqs_queue.production_dlq.arn}
```

## Configuration for Published Version

```yaml
resource:
  aws_lambda_function_event_invoke_config:
    example:
      function_name: ${aws_lambda_function.example.function_name}
      qualifier: ${aws_lambda_function.example.version}
      maximum_event_age_in_seconds: 21600
      maximum_retry_attempts: 2
      destination_config:
        on_failure:
          destination: ${aws_sqs_queue.version_dlq.arn}
        on_success:
          destination: ${aws_sns_topic.version_success.arn}
```

## Configuration for Latest Version

```yaml
resource:
  aws_lambda_function_event_invoke_config:
    example:
      function_name: ${aws_lambda_function.example.function_name}
      qualifier: $LATEST
      maximum_event_age_in_seconds: 120
      maximum_retry_attempts: 0
      destination_config:
        on_failure:
          destination: ${aws_sqs_queue.dev_dlq.arn}
```

## Multiple Destination Types

```yaml
resource:
  aws_s3_bucket:
    lambda_success_archive:
      bucket: "lambda-success-archive-${random_id.bucket_suffix.hex}"

resource:
  aws_cloudwatch_event_bus:
    lambda_failures:
      name: lambda-failure-events

resource:
  aws_lambda_function_event_invoke_config:
    example:
      function_name: ${aws_lambda_function.example.function_name}
      destination_config:
        on_failure:
          destination: ${aws_cloudwatch_event_bus.lambda_failures.arn}
        on_success:
          destination: ${aws_s3_bucket.lambda_success_archive.arn}
```
