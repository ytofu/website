# Lambda Event Source Mapping

Manage Lambda Event Source Mapping resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lambda_event_source_mapping:
    example:
      event_source_arn: ${aws_dynamodb_table.example.stream_arn}
      function_name: ${aws_lambda_function.example.arn}
      starting_position: LATEST
      tags:
        Name: dynamodb-stream-mapping
```

## Kinesis Stream

```yaml
resource:
  aws_lambda_event_source_mapping:
    example:
      event_source_arn: ${aws_kinesis_stream.example.arn}
      function_name: ${aws_lambda_function.example.arn}
      starting_position: LATEST
      batch_size: 100
      maximum_batching_window_in_seconds: 5
      parallelization_factor: 2
      destination_config:
        on_failure:
          destination_arn: ${aws_sqs_queue.dlq.arn}
```

## SQS Queue

```yaml
resource:
  aws_lambda_event_source_mapping:
    example:
      event_source_arn: ${aws_sqs_queue.example.arn}
      function_name: ${aws_lambda_function.example.arn}
      batch_size: 10
      scaling_config:
        maximum_concurrency: 100
```

## SQS with Event Filtering

```yaml
resource:
  aws_lambda_event_source_mapping:
    example:
      event_source_arn: ${aws_sqs_queue.example.arn}
      function_name: ${aws_lambda_function.example.arn}
      filter_criteria:
        filter:
          pattern: '{ "body": { "Temperature": [{ "numeric": [">", 0, "<=", 100] }] "Location": ["New York"] } }'
```

## Amazon MSK

```yaml
resource:
  aws_lambda_event_source_mapping:
    example:
      event_source_arn: ${aws_msk_cluster.example.arn}
      function_name: ${aws_lambda_function.example.arn}
      topics: 
        - orders
        - inventory
      starting_position: TRIM_HORIZON
      batch_size: 100
      amazon_managed_kafka_event_source_config:
        consumer_group_id: lambda-consumer-group
```

## Self-Managed Apache Kafka

```yaml
resource:
  aws_lambda_event_source_mapping:
    example:
      function_name: ${aws_lambda_function.example.arn}
      topics: 
        - orders
      starting_position: TRIM_HORIZON
      self_managed_event_source:
        endpoints:
          KAFKA_BOOTSTRAP_SERVERS: "kafka1.example.com:9092,kafka2.example.com:9092"
      self_managed_kafka_event_source_config:
        consumer_group_id: lambda-consumer-group
      source_access_configuration:
        type: VPC_SUBNET
        uri: "subnet:${aws_subnet.example1.id}"
      source_access_configuration:
        type: VPC_SUBNET
        uri: "subnet:${aws_subnet.example2.id}"
      source_access_configuration:
        type: VPC_SECURITY_GROUP
        uri: "security_group:${aws_security_group.example.id}"
      provisioned_poller_config:
        maximum_pollers: 100
        minimum_pollers: 10
        poller_group_name: group-123
```

## Amazon MQ (ActiveMQ)

```yaml
resource:
  aws_lambda_event_source_mapping:
    example:
      event_source_arn: ${aws_mq_broker.example.arn}
      function_name: ${aws_lambda_function.example.arn}
      queues: 
        - orders
      batch_size: 10
      source_access_configuration:
        type: BASIC_AUTH
        uri: ${aws_secretsmanager_secret_version.example.arn}
```

## Amazon MQ (RabbitMQ)

```yaml
resource:
  aws_lambda_event_source_mapping:
    example:
      event_source_arn: ${aws_mq_broker.example.arn}
      function_name: ${aws_lambda_function.example.arn}
      queues: 
        - orders
      batch_size: 1
      source_access_configuration:
        type: VIRTUAL_HOST
        uri: /production
      source_access_configuration:
        type: BASIC_AUTH
        uri: ${aws_secretsmanager_secret_version.example.arn}
```

## DocumentDB Change Stream

```yaml
resource:
  aws_lambda_event_source_mapping:
    example:
      event_source_arn: ${aws_docdb_cluster.example.arn}
      function_name: ${aws_lambda_function.example.arn}
      starting_position: LATEST
      document_db_event_source_config:
        database_name: orders
        collection_name: transactions
        full_document: UpdateLookup
      source_access_configuration:
        type: BASIC_AUTH
        uri: ${aws_secretsmanager_secret_version.example.arn}
```
