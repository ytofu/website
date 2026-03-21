# MSK Cluster Policy

Manage MSK Cluster Policy resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

data:
  aws_partition:
    current:

resource:
  aws_msk_cluster_policy:
    example:
      cluster_arn: ${aws_msk_cluster.example.arn}
      policy: '{ "Version": "2012-10-17", "Statement": [{ "Sid": "ExampleMskClusterPolicy" "Effect": "Allow" "Principal": { "AWS" = "arn:${data.aws_partition.current.partition}:iam::${data.aws_caller_identity.current.account_id}:root" } "Action": [ "kafka:Describe*", "kafka:Get*", "kafka:CreateVpcConnection", "kafka:GetBootstrapBrokers", ] "Resource": aws_msk_cluster.example.arn }] }'
```
