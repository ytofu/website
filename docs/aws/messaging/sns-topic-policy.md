# Resource: aws_sns_topic_policy

Provides an SNS topic policy resource

## Basic Example

```yaml
resource:
  aws_sns_topic:
    test:
      name: my-topic-with-policy

resource:
  aws_sns_topic_policy:
    default:
      arn: ${aws_sns_topic.test.arn}
      policy: ${data.aws_iam_policy_document.sns_topic_policy.json}

data:
  aws_iam_policy_document:
    sns_topic_policy:
      policy_id: __default_policy_ID
      statement:
        actions:
          - "SNS:Subscribe"
          - "SNS:SetTopicAttributes"
          - "SNS:RemovePermission"
          - "SNS:Receive"
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
          - ${aws_sns_topic.test.arn}
        sid: __default_statement_ID
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `arn` - (Required) The ARN of the SNS topic
* `policy` - (Required) The fully-formed AWS policy as JSON. For more information about building AWS IAM policy documents with ytofu, see the [AWS IAM Policy Document Guide](https://learn.hashicorp.com/terraform/aws/iam-policy).

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `owner` - The AWS Account ID of the SNS topic owner

## Import

```bash
ytofu import aws_sns_topic_policy.user_updates arn:aws:sns:us-west-2:123456789012:my-topic
```
