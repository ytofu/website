# Observabilityadmin Telemetry Pipeline

Manage Observabilityadmin Telemetry Pipeline resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

data:
  aws_partition:
    current:

resource:
  aws_iam_role:
    example:
      name: example-telemetry-pipeline
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [{ "Action": "sts:AssumeRole" "Effect": "Allow" "Principal": { "Service": "observabilityadmin.amazonaws.com" } }] }'

resource:
  aws_iam_role_policy:
    example:
      role: ${aws_iam_role.example.name}
      policy: '{ "Version": "2012-10-17" "Statement": [{ "Effect": "Allow" "Action": [ "logs:CreateLogGroup", "logs:CreateLogStream", "logs:PutLogEvents", "logs:DescribeLogGroups", "logs:DescribeLogStreams", ] "Resource": "arn:${data.aws_partition.current.partition}:logs:*:${data.aws_caller_identity.current.account_id}:*" }] }'

resource:
  aws_observabilityadmin_telemetry_pipeline:
    example:
      name: example-pipeline
      configuration:
        body: '# yamlencode content'
      depends_on:
        - ${aws_iam_role_policy.example}
```

## Pipeline with Processor

```yaml
resource:
  aws_observabilityadmin_telemetry_pipeline:
    example:
      name: example-vpc-pipeline
      configuration:
        body: '# yamlencode content'
      depends_on: 
        - ${aws_iam_role_policy.example}
```
