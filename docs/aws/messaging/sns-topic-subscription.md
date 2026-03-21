# SNS Topic Subscription

Manage SNS Topic Subscription resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sns_topic:
    user_updates:
      name: user-updates-topic

resource:
  aws_sqs_queue:
    user_updates_queue:
      name: user-updates-queue
      policy: ${data.aws_iam_policy_document.sqs_queue_policy.json}

resource:
  aws_sns_topic_subscription:
    user_updates_sqs_target:
      topic_arn: ${aws_sns_topic.user_updates.arn}
      protocol: sqs
      endpoint: ${aws_sqs_queue.user_updates_queue.arn}

data:
  aws_iam_policy_document:
    sqs_queue_policy:
      policy_id: "arn:aws:sqs:us-west-2:123456789012:user_updates_queue/SQSDefaultPolicy"
      statement:
        sid: user_updates_sqs_target
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - sns.amazonaws.com
        actions:
          - "SQS:SendMessage"
        resources:
          - "arn:aws:sqs:us-west-2:123456789012:user-updates-queue"
        condition:
          test: ArnEquals
          values:
            - ${aws_sns_topic.user_updates.arn}
```

## Example Cross-account Subscription

```yaml
data:
  aws_iam_policy_document:
    sns_topic_policy:
      policy_id: __default_policy_ID
      statement:
        actions:
          - "SNS:Subscribe"
          - "SNS:SetTopicAttributes"
          - "SNS:RemovePermission"
          - "SNS:Publish"
          - "SNS:ListSubscriptionsByTopic"
          - "SNS:GetTopicAttributes"
          - "SNS:DeleteTopic"
          - "SNS:AddPermission"
        condition:
          test: StringEquals
          values:
            - example-value
        effect: Allow
        principals:
          type: AWS
          identifiers: 
            - "*"
        resources:
          - "arn:aws:sns:example-value:example-value:example-value"
        sid: __default_statement_ID
      statement:
        actions:
          - "SNS:Subscribe"
          - "SNS:Receive"
        condition:
          test: StringLike
          values:
            - "arn:aws:sqs:example-value:example-value:example-value"
        effect: Allow
        principals:
          type: AWS
          identifiers: 
            - "*"
        resources:
          - "arn:aws:sns:example-value:example-value:example-value"
        sid: __console_sub_0

data:
  aws_iam_policy_document:
    sqs_queue_policy:
      policy_id: "arn:aws:sqs:example-value:example-value:example-value/SQSDefaultPolicy"
      statement:
        sid: example-sns-topic
        effect: Allow
        principals:
          type: AWS
          identifiers: 
            - "*"
        actions:
          - "SQS:SendMessage"
        resources:
          - "arn:aws:sqs:example-value:example-value:example-value"
        condition:
          test: ArnEquals
          values:
            - "arn:aws:sns:example-value:example-value:example-value"

resource:
  aws_sns_topic:
    sns_topic:
      name: example-value
      display_name: example-value
      policy: ${data.aws_iam_policy_document.sns_topic_policy.json}

resource:
  aws_sqs_queue:
    sqs_queue:
      name: example-value
      policy: ${data.aws_iam_policy_document.sqs_queue_policy.json}

resource:
  aws_sns_topic_subscription:
    sns_topic:
      topic_arn: ${aws_sns_topic.sns_topic.arn}
      protocol: sqs
      endpoint: ${aws_sqs_queue.sqs_queue.arn}
```

## Example with Delivery Policy

```yaml
resource:
  aws_sns_topic_subscription:
    example_with_delivery_policy:
      topic_arn: "arn:aws:sns:us-west-2:123456789012:my-topic"
      protocol: https
      endpoint: "https://example.com/endpoint"
      raw_message_delivery: true
      delivery_policy: |
        {
        "healthyRetryPolicy": {
        "minDelayTarget": 20,
        "maxDelayTarget": 20,
        "numRetries": 3,
        "numMaxDelayRetries": 0,
        "numNoDelayRetries": 0,
        "numMinDelayRetries": 0,
        "backoffFunction": "linear"
        },
        "sicklyRetryPolicy": null,
        "throttlePolicy": null,
        "requestPolicy": {
        "headerContentType": "text/plain; application/json"
        },
        "guaranteed": false
        }
```
