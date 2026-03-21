# Kinesis Stream Consumer

Manage Kinesis Stream Consumer resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_kinesis_stream:
    example:
      name: example-stream
      shard_count: 1

resource:
  aws_kinesis_stream_consumer:
    example:
      name: example-consumer
      stream_arn: ${aws_kinesis_stream.example.arn}
```
