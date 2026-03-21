# Resource: aws_lambda_function_event_invoke_config

Manages an AWS Lambda Function Event Invoke Config. Use this resource to configure error handling and destinations for asynchronous Lambda function invocations.

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

## Argument Reference

The following arguments are required:

* `function_name` - (Required) Name or ARN of the Lambda Function, omitting any version or alias qualifier.

The following arguments are optional:

* `destination_config` - (Optional) Configuration block with destination configuration. [See below](#destination_config-configuration-block).
* `maximum_event_age_in_seconds` - (Optional) Maximum age of a request that Lambda sends to a function for processing in seconds. Valid values between 60 and 21600.
* `maximum_retry_attempts` - (Optional) Maximum number of times to retry when the function returns an error. Valid values between 0 and 2. Defaults to 2.
* `qualifier` - (Optional) Lambda Function published version, `$LATEST`, or Lambda Alias name.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

### destination_config Configuration Block

* `on_failure` - (Optional) Configuration block with destination configuration for failed asynchronous invocations. [See below](#destination_config-on_failure-configuration-block).
* `on_success` - (Optional) Configuration block with destination configuration for successful asynchronous invocations. [See below](#destination_config-on_success-configuration-block).

#### destination_config on_failure Configuration Block

* `destination` - (Required) ARN of the destination resource. See the [Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/invocation-async.html#invocation-async-destinations) for acceptable resource types and associated IAM permissions.

#### destination_config on_success Configuration Block

* `destination` - (Required) ARN of the destination resource. See the [Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/invocation-async.html#invocation-async-destinations) for acceptable resource types and associated IAM permissions.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Fully qualified Lambda Function name or ARN.
