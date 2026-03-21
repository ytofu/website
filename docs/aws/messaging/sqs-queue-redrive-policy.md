# Resource: aws_sqs_queue_redrive_policy

Allows you to set a redrive policy of an SQS Queue
while referencing ARN of the dead letter queue inside the redrive policy.

## Basic Example

```yaml
resource:
  aws_sqs_queue:
    q:
      name: examplequeue

  aws_sqs_queue:
    ddl:
      name: examplequeue-ddl
      redrive_allow_policy: '{ "redrivePermission": "byQueue", "sourceQueueArns": [aws_sqs_queue.q.arn] }'

  aws_sqs_queue_redrive_policy:
    q:
      queue_url: ${aws_sqs_queue.q.id}
      redrive_policy: '{ "deadLetterTargetArn": aws_sqs_queue.ddl.arn "maxReceiveCount": 4 }'```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `queue_url` - (Required) The URL of the SQS Queue to which to attach the policy
* `redrive_policy` - (Required) The JSON redrive policy for the SQS queue. Accepts two key/val pairs: `deadLetterTargetArn` and `maxReceiveCount`. Learn more in the [Amazon SQS dead-letter queues documentation](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-dead-letter-queues.html).

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_sqs_queue_redrive_policy.test https://queue.amazonaws.com/123456789012/myqueue
```
