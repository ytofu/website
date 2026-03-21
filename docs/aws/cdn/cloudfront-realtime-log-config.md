# Cloudfront Realtime Log Config

Manage Cloudfront Realtime Log Config resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - cloudfront.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    example:
      name: cloudfront-realtime-log-config-example
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

data:
  aws_iam_policy_document:
    example:
      statement:
        effect: Allow
        actions:
          - "kinesis:DescribeStreamSummary"
          - "kinesis:DescribeStream"
          - "kinesis:PutRecord"
          - "kinesis:PutRecords"
        resources: 
          - ${aws_kinesis_stream.example.arn}

resource:
  aws_iam_role_policy:
    example:
      name: cloudfront-realtime-log-config-example
      role: ${aws_iam_role.example.id}
      policy: ${data.aws_iam_policy_document.example.json}

resource:
  aws_cloudfront_realtime_log_config:
    example:
      name: example
      sampling_rate: 75
      fields: 
        - timestamp
        - c-ip
      endpoint:
        stream_type: Kinesis
        kinesis_stream_config:
          role_arn: ${aws_iam_role.example.arn}
          stream_arn: ${aws_kinesis_stream.example.arn}
      depends_on: 
        - ${aws_iam_role_policy.example}
```
