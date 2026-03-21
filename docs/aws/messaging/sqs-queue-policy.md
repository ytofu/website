# Resource: aws_sqs_queue_policy

Allows you to set a policy of an SQS Queue while referencing the ARN of the queue within the policy.

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `policy` - (Required) JSON policy for the SQS queue. For more information about building AWS IAM policy documents with ytofu, see the [AWS IAM Policy Document Guide](https://learn.hashicorp.com/terraform/aws/iam-policy). Ensure that `Version = "2012-10-17"` is set in the policy or AWS may hang in creating the queue.
* `queue_url` - (Required) URL of the SQS Queue to which to attach the policy.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_sqs_queue_policy.test https://queue.amazonaws.com/123456789012/myqueue
```
