# Resource: aws_kinesis_resource_policy

Provides a resource to manage an Amazon Kinesis Streams resource policy.
Use a resource policy to manage cross-account access to your data streams or consumers.

## Basic Example

```yaml
resource:
  aws_kinesis_resource_policy:
    example:
      resource_arn: ${aws_kinesis_stream.example.arn}
      policy: |
        {
        "Version": "2012-10-17",
        "Id": "writePolicy",
        "Statement": [{
        "Sid": "writestatement",
        "Effect": "Allow",
        "Principal": {
        "AWS": "123456789456"
        },
        "Action": [
        "kinesis:DescribeStreamSummary",
        "kinesis:ListShards",
        "kinesis:PutRecord",
        "kinesis:PutRecords"
        ],
        "Resource": "${aws_kinesis_stream.example.arn}"
        }]
        }
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `policy` - (Required) The policy document.
* `resource_arn` - (Required) The Amazon Resource Name (ARN) of the data stream or consumer.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_kinesis_resource_policy.example arn:aws:kinesis:us-west-2:123456789012:stream/example
```
