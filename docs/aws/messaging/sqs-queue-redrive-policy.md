# SQS Queue Redrive Policy

Manage SQS Queue Redrive Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sqs_queue:
    q:
      name: examplequeue

resource:
  aws_sqs_queue:
    ddl:
      name: examplequeue-ddl
      redrive_allow_policy: '{ "redrivePermission": "byQueue", "sourceQueueArns": [aws_sqs_queue.q.arn] }'

resource:
  aws_sqs_queue_redrive_policy:
    q:
      queue_url: ${aws_sqs_queue.q.id}
      redrive_policy: '{ "deadLetterTargetArn": aws_sqs_queue.ddl.arn "maxReceiveCount": 4 }'
```
