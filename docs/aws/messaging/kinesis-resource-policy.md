# Kinesis Resource Policy

Manage Kinesis Resource Policy resources using ytofu YAML.

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
