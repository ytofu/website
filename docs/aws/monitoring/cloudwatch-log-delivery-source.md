# Resource: aws_cloudwatch_log_delivery_source

ytofu resource for managing an AWS CloudWatch Logs Delivery Source.

## Basic Example

```yaml
resource:
  aws_cloudwatch_log_delivery_source:
    example:
      name: example
      log_type: APPLICATION_LOGS
      resource_arn: ${aws_bedrockagent_knowledge_base.example.arn}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `log_type` - (Required) The type of log that the source is sending. For Amazon Bedrock, the valid value is `APPLICATION_LOGS`. For Amazon CodeWhisperer, the valid value is `EVENT_LOGS`. For IAM Identity Center, the valid value is `ERROR_LOGS`. For Amazon WorkMail, the valid values are `ACCESS_CONTROL_LOGS`, `AUTHENTICATION_LOGS`, `WORKMAIL_AVAILABILITY_PROVIDER_LOGS`, and `WORKMAIL_MAILBOX_ACCESS_LOGS`.
* `name` - (Required) The name for this delivery source.
* `resource_arn` - (Required) The ARN of the AWS resource that is generating and sending logs.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The Amazon Resource Name (ARN) of the delivery source.
* `service` - The AWS service that is sending logs.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_cloudwatch_log_delivery_source.example example
```
