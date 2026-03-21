# Resource: aws_sns_topic_data_protection_policy

Provides an SNS data protection topic policy resource

## Basic Example

```yaml
resource:
  aws_sns_topic:
    example:
      name: example

resource:
  aws_sns_topic_data_protection_policy:
    example:
      arn: ${aws_sns_topic.example.arn}
      policy: 'example-json-policy'
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `arn` - (Required) The ARN of the SNS topic
* `policy` - (Required) The fully-formed AWS policy as JSON. For more information about building AWS IAM policy documents with ytofu, see the [AWS IAM Policy Document Guide](https://learn.hashicorp.com/terraform/aws/iam-policy).

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

## Import

```bash
ytofu import aws_sns_topic_data_protection_policy.example arn:aws:sns:us-west-2:123456789012:example
```
