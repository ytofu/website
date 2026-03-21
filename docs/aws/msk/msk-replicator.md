# MSK Replicator

Manage MSK Replicator resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_msk_replicator:
    test:
      replicator_name: test-name
      description: test-description
      service_execution_role_arn: ${aws_iam_role.source.arn}
      kafka_cluster:
        amazon_msk_cluster:
          msk_cluster_arn: ${aws_msk_cluster.source.arn}
        vpc_config:
          subnet_ids: ${aws_subnet.source[*].id}
          security_groups_ids: 
            - ${aws_security_group.source.id}
      kafka_cluster:
        amazon_msk_cluster:
          msk_cluster_arn: ${aws_msk_cluster.target.arn}
        vpc_config:
          subnet_ids: ${aws_subnet.target[*].id}
          security_groups_ids: 
            - ${aws_security_group.target.id}
      replication_info_list:
        source_kafka_cluster_arn: ${aws_msk_cluster.source.arn}
        target_kafka_cluster_arn: ${aws_msk_cluster.target.arn}
        target_compression_type: NONE
        topic_replication:
          topic_name_configuration:
            type: PREFIXED_WITH_SOURCE_CLUSTER_ALIAS
          topics_to_replicate: 
            - ".*"
          starting_position:
            type: LATEST
        consumer_group_replication:
          consumer_groups_to_replicate: 
            - ".*"
```
