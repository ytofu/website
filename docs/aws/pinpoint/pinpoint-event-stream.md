# Pinpoint Event Stream

Manage Pinpoint Event Stream resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_pinpoint_event_stream:
    stream:
      application_id: ${aws_pinpoint_app.app.application_id}
      destination_stream_arn: ${aws_kinesis_stream.test_stream.arn}
      role_arn: ${aws_iam_role.test_role.arn}

resource:
  aws_pinpoint_app:
    app:

resource:
  aws_kinesis_stream:
    test_stream:
      name: pinpoint-kinesis-test
      shard_count: 1

data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - pinpoint.us-east-1.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    test_role:
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

data:
  aws_iam_policy_document:
    test_role_policy:
      statement:
        effect: Allow
        actions:
          - "kinesis:PutRecords"
          - "kinesis:DescribeStream"
        resources: 
          - "arn:aws:kinesis:us-east-1:*:*/*"

resource:
  aws_iam_role_policy:
    test_role_policy:
      name: test_policy
      role: ${aws_iam_role.test_role.id}
      policy: ${data.aws_iam_policy_document.test_role_policy.json}
```
