# SQS Queue Policy

Manage SQS Queue Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sqs_queue:
    q:
      name: examplequeue

data:
  aws_iam_policy_document:
    test:
      statement:
        sid: First
        effect: Allow
        principals:
          type: "*"
          identifiers: 
            - "*"
        actions: 
          - "sqs:SendMessage"
        resources: 
          - ${aws_sqs_queue.q.arn}
        condition:
          test: ArnEquals
          values: 
            - ${aws_sns_topic.example.arn}

resource:
  aws_sqs_queue_policy:
    test:
      queue_url: ${aws_sqs_queue.q.id}
      policy: ${data.aws_iam_policy_document.test.json}
```

## Timeout Problems Creating/Updating

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: brodobaggins

resource:
  aws_sqs_queue:
    example:
      name: be-giant

resource:
  aws_sqs_queue_policy:
    example:
      queue_url: ${aws_sqs_queue.example.id}
      policy: '{ "Version": "2012-10-17" # !! Important !! "Statement": [{ "Sid": "Cejuwdam" "Effect": "Allow" "Principal": { "Service": "s3.amazonaws.com" } "Action": "SQS:SendMessage" "Resource": aws_sqs_queue.example.arn "Condition": { "ArnLike": { "aws:SourceArn" = aws_s3_bucket.example.arn } } }] }'
```
