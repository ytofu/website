# Resource: aws_sns_topic_subscription

Provides a resource for subscribing to SNS topics. Requires that an SNS topic exist for the subscription to attach to. This resource allows you to automatically place messages sent to SNS topics in SQS queues, send them as HTTP(S) POST requests to a given endpoint, send SMS messages, or notify devices / applications. The most likely use case for ytofu users will probably be SQS queues.

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

## Argument Reference

The following arguments are required:

* `endpoint` - (Required) Endpoint to send data to. The contents vary with the protocol. See details below.
* `protocol` - (Required) Protocol to use. Valid values are: `sqs`, `sms`, `lambda`, `firehose`, and `application`. Protocols `email`, `email-json`, `http` and `https` are also valid but partially supported. See details below.
* `subscription_role_arn` - (Required if `protocol` is `firehose`) ARN of the IAM role to publish to Kinesis Data Firehose delivery stream. Refer to [SNS docs](https://docs.aws.amazon.com/sns/latest/dg/sns-firehose-as-subscriber.html).
* `topic_arn` - (Required) ARN of the SNS topic to subscribe to.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `confirmation_timeout_in_minutes` - (Optional) Integer indicating number of minutes to wait in retrying mode for fetching subscription arn before marking it as failure. Only applicable for http and https protocols. Default is `1`.
* `delivery_policy` - (Optional) JSON String with the delivery policy (retries, backoff, etc.) that will be used in the subscription - this only applies to HTTP/S subscriptions. Refer to the [SNS docs](https://docs.aws.amazon.com/sns/latest/dg/DeliveryPolicies.html) for more details.
* `endpoint_auto_confirms` - (Optional) Whether the endpoint is capable of [auto confirming subscription](http://docs.aws.amazon.com/sns/latest/dg/SendMessageToHttp.html#SendMessageToHttp.prepare) (e.g., PagerDuty). Default is `false`.
* `filter_policy` - (Optional) JSON String with the filter policy that will be used in the subscription to filter messages seen by the target resource. Refer to the [SNS docs](https://docs.aws.amazon.com/sns/latest/dg/message-filtering.html) for more details.
* `filter_policy_scope` - (Optional) Whether the `filter_policy` applies to `MessageAttributes` (default) or `MessageBody`.
* `raw_message_delivery` - (Optional) Whether to enable raw message delivery (the original message is directly passed, not wrapped in JSON with the original message in the message property). Default is `false`.
* `redrive_policy` - (Optional) JSON String with the redrive policy that will be used in the subscription. Refer to the [SNS docs](https://docs.aws.amazon.com/sns/latest/dg/sns-dead-letter-queues.html#how-messages-moved-into-dead-letter-queue) for more details.
* `replay_policy` - (Optional) JSON String with the archived message replay policy that will be used in the subscription. Refer to the [SNS docs](https://docs.aws.amazon.com/sns/latest/dg/message-archiving-and-replay-subscriber.html) for more details.

### Protocol support

Supported values for `protocol` include:

* `application` - Delivers JSON-encoded messages. `endpoint` is the endpoint ARN of a mobile app and device.
* `firehose` - Delivers JSON-encoded messages. `endpoint` is the ARN of an Amazon Kinesis Data Firehose delivery stream (e.g.,
`arn:aws:firehose:us-east-1:123456789012:deliverystream/ticketUploadStream`).
* `lambda` - Delivers JSON-encoded messages. `endpoint` is the ARN of an AWS Lambda function.
* `sms` - Delivers text messages via SMS. `endpoint` is the phone number of an SMS-enabled device.
* `sqs` - Delivers JSON-encoded messages. `endpoint` is the ARN of an Amazon SQS queue (e.g., `arn:aws:sqs:us-west-2:123456789012:terraform-queue-too`).

Partially supported values for `protocol` include:

* `email` - Delivers messages via SMTP. `endpoint` is an email address.
* `email-json` - Delivers JSON-encoded messages via SMTP. `endpoint` is an email address.
* `http` -- Delivers JSON-encoded messages via HTTP POST. `endpoint` is a URL beginning with `http://`.
* `https` -- Delivers JSON-encoded messages via HTTPS POST. `endpoint` is a URL beginning with `https://`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the subscription.
* `confirmation_was_authenticated` - Whether the subscription confirmation request was authenticated.
* `id` - ARN of the subscription.
* `owner_id` - AWS account ID of the subscription's owner.
* `pending_confirmation` - Whether the subscription has not been confirmed.

## Import

```bash
ytofu import aws_sns_topic_subscription.user_updates_sqs_target arn:aws:sns:us-west-2:123456789012:my-topic:8a21d249-4329-4871-acc6-7be709c6ea7f
```
