# Resource: aws_msk_cluster_policy

ytofu resource for managing an AWS Managed Streaming for Kafka Cluster Policy.

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `cluster_arn` - (Required) The Amazon Resource Name (ARN) that uniquely identifies the cluster.
* `policy` - (Required) Resource policy for cluster.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Same as `cluster_arn`.

## Import

```bash
ytofu import aws_msk_cluster_policy.example arn:aws:kafka:us-west-2:123456789012:cluster/example/279c0212-d057-4dba-9aa9-1c4e5a25bfc7-3
```
