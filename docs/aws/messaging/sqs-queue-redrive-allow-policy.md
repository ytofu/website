# SQS Queue Redrive Allow Policy

Manage SQS Queue Redrive Allow Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sqs_queue:
    src:
      name: srcqueue
      redrive_policy: '{ "deadLetterTargetArn": aws_sqs_queue.example.arn "maxReceiveCount": 4 }'

resource:
  aws_sqs_queue:
    example:
      name: examplequeue

resource:
  aws_sqs_queue_redrive_allow_policy:
    example:
      queue_url: ${aws_sqs_queue.example.id}
      redrive_allow_policy: '{ "redrivePermission": "byQueue", "sourceQueueArns": [aws_sqs_queue.src.arn] }'
```
