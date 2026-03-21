# Resource: aws_kinesis_stream_consumer

Provides a resource to manage a Kinesis Stream Consumer.

## Basic Example

```yaml
resource:
  aws_kinesis_stream:
    example:
      name: example-stream
      shard_count: 1

  aws_kinesis_stream_consumer:
    example:
      name: example-consumer
      stream_arn: ${aws_kinesis_stream.example.arn}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required, Forces new resource) Name of the stream consumer.
* `stream_arn` - (Required, Forces new resource) Amazon Resource Name (ARN) of the data stream the consumer is registered with.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) of the stream consumer.
* `creation_timestamp` - Approximate timestamp in [RFC3339 format](https://tools.ietf.org/html/rfc3339#section-5.8) of when the stream consumer was created.
* `id` - Amazon Resource Name (ARN) of the stream consumer.

## Import

```bash
ytofu import aws_kinesis_stream_consumer.example arn:aws:kinesis:us-west-2:123456789012:stream/example/consumer/example:1616044553
```
