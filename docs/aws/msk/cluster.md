# MSK Cluster

Create managed Kafka clusters using ytofu YAML.

## Basic Cluster

```yaml
resource:
  aws_msk_cluster:
    example:
      cluster_name: example
      kafka_version: "3.5.1"
      number_of_broker_nodes: 3
      broker_node_group_info:
        instance_type: kafka.m5.large
        client_subnets:
          - ${aws_subnet.a.id}
          - ${aws_subnet.b.id}
          - ${aws_subnet.c.id}
        storage_info:
          ebs_storage_info:
            volume_size: 100
        security_groups:
          - ${aws_security_group.msk.id}
      tags:
        Environment: production
```

## With Encryption

```yaml
resource:
  aws_msk_cluster:
    example:
      cluster_name: example
      kafka_version: "3.5.1"
      number_of_broker_nodes: 3
      broker_node_group_info:
        instance_type: kafka.m5.large
        client_subnets:
          - ${aws_subnet.a.id}
          - ${aws_subnet.b.id}
          - ${aws_subnet.c.id}
        storage_info:
          ebs_storage_info:
            volume_size: 100
        security_groups:
          - ${aws_security_group.msk.id}
      encryption_info:
        encryption_at_rest_kms_key_arn: ${aws_kms_key.msk.arn}
        encryption_in_transit:
          client_broker: TLS
          in_cluster: true
```

## With Logging

```yaml
resource:
  aws_msk_cluster:
    example:
      cluster_name: example
      kafka_version: "3.5.1"
      number_of_broker_nodes: 3
      broker_node_group_info:
        instance_type: kafka.m5.large
        client_subnets:
          - ${aws_subnet.a.id}
          - ${aws_subnet.b.id}
          - ${aws_subnet.c.id}
        security_groups:
          - ${aws_security_group.msk.id}
      logging_info:
        broker_logs:
          cloudwatch_logs:
            enabled: true
            log_group: /aws/msk/cluster
          s3_logs:
            enabled: true
            bucket: ${aws_s3_bucket.msk_logs.id}
            prefix: logs/msk-
```
