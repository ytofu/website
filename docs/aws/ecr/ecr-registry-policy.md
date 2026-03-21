# ECR Registry Policy

Manage ECR Registry Policy resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

data:
  aws_region:
    current:

data:
  aws_partition:
    current:

resource:
  aws_ecr_registry_policy:
    example:
      policy: '{ "Version": "2012-10-17", "Statement": [ { "Sid": "testpolicy", "Effect": "Allow", "Principal": { "AWS" : "arn:${data.aws_partition.current.partition}:iam::${data.aws_caller_identity.current.account_id}:root" }, "Action": [ "ecr:ReplicateImage" ], "Resource": [ "arn:${data.aws_partition.current.partition}:ecr:${data.aws_region.current.region}:${data.aws_caller_identity.current.account_id}:repository/*" ] } ] }'
```
