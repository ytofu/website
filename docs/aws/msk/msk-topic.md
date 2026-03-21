# Resource: aws_msk_topic

Manages an AWS Managed Streaming for Kafka Topic.

## Basic Example

```yaml
resource:
  aws_msk_topic:
    example:
      name: Example
      cluster_arn: ${aws_msk_cluster.example.arn}
      partition_count: 2
      replication_factor: 2
      configs: '{ "retention.ms" = "604800000" "retention.bytes" = "-1", "cleanup.policy" = "delete", "min.insync.replicas" = "2" }'
```

## Argument Reference

The following arguments are required:

* `cluster_arn` - (Required) Amazon Resource Name (ARN) that uniquely identifies MSK Cluster.
* `name` - (Required) Name of Topic.
* `partition_count` - (Required) Number of partitions for Topic.
* `replication_factor` - (Required) Replication factor for Topic.

The following arguments are optional:

* `configs` - (Optional) Explicit configured Kafka configuration in JSON format for Topic.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Topic.
* `configs_actual` - Aggregated Kafka configuration in JSON format for Topic, both explicit set values from `configs` and implicit set values (AWS default configuration, historically set values or manual configuration from outside ytofu).

## Timeouts

Configuration options:

* `create` - (Default `30m`)
* `update` - (Default `30m`)
* `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_kafka_topic.example arn:aws:kafka:us-west-2:123456789012:cluster/example/279c0212-d057-4dba-9aa9-1c4e5a25bfc7-3,topicname
```
