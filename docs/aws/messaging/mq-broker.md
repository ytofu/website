# MQ Broker

Manage MQ Broker resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_mq_broker:
    example:
      broker_name: example
      configuration:
        id: ${aws_mq_configuration.test.id}
        revision: ${aws_mq_configuration.test.latest_revision}
      engine_type: ActiveMQ
      engine_version: 5.17.6
      host_instance_type: mq.t2.micro
      security_groups: 
        - ${aws_security_group.test.id}
      user:
        username: example_user
        password: <password>
```

## High-throughput Optimized Example

```yaml
resource:
  aws_mq_broker:
    example:
      broker_name: example
      configuration:
        id: ${aws_mq_configuration.test.id}
        revision: ${aws_mq_configuration.test.latest_revision}
      engine_type: ActiveMQ
      engine_version: 5.17.6
      storage_type: ebs
      host_instance_type: mq.m5.large
      security_groups: 
        - ${aws_security_group.test.id}
      user:
        username: example_user
        password: <password>
```

## Cross-Region Data Replication

```yaml
resource:
  aws_mq_broker:
    example_primary:
      apply_immediately: true
      broker_name: example_primary
      engine_type: ActiveMQ
      engine_version: 5.17.6
      host_instance_type: mq.m5.large
      security_groups: 
        - ${aws_security_group.example_primary.id}
      deployment_mode: ACTIVE_STANDBY_MULTI_AZ
      user:
        username: example_user
        password: <password>
      user:
        username: example_replication_user
        password: <password>
        replication_user: true

resource:
  aws_mq_broker:
    example:
      apply_immediately: true
      broker_name: example
      engine_type: ActiveMQ
      engine_version: 5.17.6
      host_instance_type: mq.m5.large
      security_groups: 
        - ${aws_security_group.example.id}
      deployment_mode: ACTIVE_STANDBY_MULTI_AZ
      data_replication_mode: CRDR
      data_replication_primary_broker_arn: ${aws_mq_broker.primary.arn}
      user:
        username: example_user
        password: <password>
      user:
        username: example_replication_user
        password: <password>
        replication_user: true
```
