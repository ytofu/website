# MQ Configuration

Manage MQ Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_mq_configuration:
    example:
      description: Example Configuration
      name: example
      engine_type: ActiveMQ
      engine_version: 5.17.6
      data: |
        <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
        <broker xmlns="http://activemq.apache.org/schema/core">
        <plugins>
        <forcePersistencyModeBrokerPlugin persistenceFlag="true"/>
        <statisticsBrokerPlugin/>
        <timeStampingBrokerPlugin ttlCeiling="86400000" zeroExpirationOverride="86400000"/>
        </plugins>
        </broker>
```

## RabbitMQ

```yaml
resource:
  aws_mq_configuration:
    example:
      description: Example Configuration
      name: example
      engine_type: RabbitMQ
      engine_version: 3.11.20
      data: |
        # Default RabbitMQ delivery acknowledgement timeout is 30 minutes in milliseconds
        consumer_timeout = 1800000
```
