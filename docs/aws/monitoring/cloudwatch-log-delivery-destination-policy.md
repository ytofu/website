# Resource: aws_cloudwatch_log_delivery_destination_policy

ytofu resource for managing an AWS CloudWatch Logs Delivery Destination Policy.

## Basic Example

```yaml
resource:
  aws_cloudwatch_log_delivery_destination_policy:
    example:
      delivery_destination_name: ${aws_cloudwatch_log_delivery_destination.example.name}
      delivery_destination_policy: ${data.aws_iam_policy_document.example.json}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `delivery_destination_name` - (Required) The name of the delivery destination to assign this policy to.
* `delivery_destination_policy` - (Required) The contents of the policy.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_cloudwatch_log_delivery_destination_policy.example example
```
