# Resource: aws_cloudwatch_log_delivery_destination

ytofu resource for managing an AWS CloudWatch Logs Delivery Destination.

## Basic Example

```yaml
resource:
  aws_cloudwatch_log_delivery_destination:
    example:
      name: example
      delivery_destination_configuration:
        destination_resource_arn: ${aws_cloudwatch_log_group.example.arn}
```

## X-Ray Trace Delivery

```yaml
resource:
  aws_cloudwatch_log_delivery_destination:
    xray:
      name: xray-traces
      delivery_destination_type: XRAY
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `delivery_destination_configuration` - (Optional) The AWS resource that will receive the logs. Required for CloudWatch Logs, Amazon S3, and Firehose destinations. Not required for X-Ray trace delivery destinations.
    * `destination_resource_arn` - (Optional) The ARN of the AWS destination that this delivery destination represents. Required when `delivery_destination_configuration` is specified.
* `delivery_destination_type` - (Optional) The type of delivery destination. Valid values: `S3`, `CWL`, `FH`, `XRAY`. Required for X-Ray trace delivery destinations. For other destination types, this is computed from the `destination_resource_arn`.
* `name` - (Required) The name for this delivery destination.
* `output_format` - (Optional) The format of the logs that are sent to this delivery destination. Valid values: `json`, `plain`, `w3c`, `raw`, `parquet`.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The Amazon Resource Name (ARN) of the delivery destination.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_cloudwatch_log_delivery_destination.example example
```
