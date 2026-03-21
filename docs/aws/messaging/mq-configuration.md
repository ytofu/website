# Resource: aws_mq_configuration

Manages an Amazon MQ configuration. Use this resource to create and manage broker configurations for ActiveMQ and RabbitMQ brokers.

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

## Argument Reference

The following arguments are required:

* `data` - (Required) Broker configuration in XML format for ActiveMQ or Cuttlefish format for RabbitMQ. See [AWS documentation](https://docs.aws.amazon.com/amazon-mq/latest/developer-guide/amazon-mq-broker-configuration-parameters.html) for supported parameters and format of the XML.
* `engine_type` - (Required) Type of broker engine. Valid values are `ActiveMQ` and `RabbitMQ`.
* `engine_version` - (Required) Version of the broker engine.
* `name` - (Required) Name of the configuration.

The following arguments are optional:

* `authentication_strategy` - (Optional) Authentication strategy associated with the configuration. Valid values are `simple` and `ldap`. `ldap` is not supported for RabbitMQ engine type.
* `description` - (Optional) Description of the configuration.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `tags` - (Optional) Key-value map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the configuration.
* `id` - Unique ID that Amazon MQ generates for the configuration.
* `latest_revision` - Latest revision of the configuration.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_mq_configuration.example c-0187d1eb-88c8-475a-9b79-16ef5a10c94f
```
