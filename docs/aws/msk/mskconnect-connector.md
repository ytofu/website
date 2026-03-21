# Mskconnect Connector

Manage Mskconnect Connector resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_mskconnect_connector:
    example:
      name: example
      kafkaconnect_version: 2.7.1
      capacity:
        autoscaling:
          mcu_count: 1
          min_worker_count: 1
          max_worker_count: 2
          scale_in_policy:
            cpu_utilization_percentage: 20
          scale_out_policy:
            cpu_utilization_percentage: 80
      connector_configuration: 
      kafka_cluster:
        apache_kafka_cluster:
          bootstrap_servers: ${aws_msk_cluster.example.bootstrap_brokers_tls}
          vpc:
            security_groups: 
              - ${aws_security_group.example.id}
            subnets: 
              - ${aws_subnet.example1.id}
              - ${aws_subnet.example2.id}
              - ${aws_subnet.example3.id}
      kafka_cluster_client_authentication:
        authentication_type: NONE
      kafka_cluster_encryption_in_transit:
        encryption_type: TLS
      plugin:
        custom_plugin:
          arn: ${aws_mskconnect_custom_plugin.example.arn}
          revision: ${aws_mskconnect_custom_plugin.example.latest_revision}
      service_execution_role_arn: ${aws_iam_role.example.arn}
```
