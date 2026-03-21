# DynamoDB Kinesis Streaming Destination

Stream DynamoDB table changes to Kinesis using ytofu YAML.

## Basic Streaming

```yaml
resource:
  aws_dynamodb_table:
    example:
      name: orders
      hash_key: id
      billing_mode: PAY_PER_REQUEST
      attribute:
        - name: id
          type: S

  aws_kinesis_stream:
    example:
      name: dynamodb-orders-stream
      shard_count: 1

  aws_dynamodb_kinesis_streaming_destination:
    example:
      stream_arn: ${aws_kinesis_stream.example.arn}
      table_name: ${aws_dynamodb_table.example.name}
```
