# Resource: aws_kinesis_stream

Provides a Kinesis Stream resource. Amazon Kinesis is a managed service that
scales elastically for real-time processing of streaming big data.

## Basic Example

```yaml
resource:
  aws_kinesis_stream:
    test_stream:
      name: terraform-kinesis-test
      shard_count: 1
      retention_period: 48
      shard_level_metrics:
        - IncomingBytes
        - OutgoingBytes
      stream_mode_details:
        stream_mode: PROVISIONED
      tags:
        Environment: test
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) A name to identify the stream. This is unique to the AWS account and region the Stream is created in.
* `shard_count` - (Optional) The number of shards that the stream will use. If the `stream_mode` is `PROVISIONED`, this field is required.
Amazon has guidelines for specifying the Stream size that should be referenced when creating a Kinesis stream. See [Amazon Kinesis Streams][2] for more.
* `retention_period` - (Optional) Length of time data records are accessible after they are added to the stream. The maximum value of a stream's retention period is 8760 hours. Minimum value is 24. Default is 24.
* `shard_level_metrics` - (Optional) A list of shard-level CloudWatch metrics which can be enabled for the stream. See [Monitoring with CloudWatch][3] for more. Note that the value ALL should not be used; instead you should provide an explicit list of metrics you wish to enable.
* `enforce_consumer_deletion` - (Optional) A boolean that indicates all registered consumers should be deregistered from the stream so that the stream can be destroyed without error. The default value is `false`.
* `encryption_type` - (Optional) The encryption type to use. The only acceptable values are `NONE` or `KMS`. The default value is `NONE`.
* `kms_key_id` - (Optional) The GUID for the customer-managed KMS key to use for encryption. You can also use a Kinesis-owned master key by specifying the alias `alias/aws/kinesis`.
* `stream_mode_details` - (Optional) Indicates the [capacity mode](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-size-a-stream.html) of the data stream. Detailed below.
* `max_record_size_in_kib` - (Optional) The maximum size for a single data record in KiB. The minimum value is 1024. The maximum value is 10240.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### stream_mode_details Configuration Block

* `stream_mode` - (Required) Specifies the capacity mode of the stream. Must be either `PROVISIONED` or `ON_DEMAND`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The unique Stream id
* `name` - The unique Stream name
* `shard_count` - The count of Shards for this Stream
* `arn` - The Amazon Resource Name (ARN) specifying the Stream (same as `id`)
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

- `create` - (Default `5m`)
- `update` - (Default `120m`)
- `delete` - (Default `120m`)

## Import

```bash
ytofu import aws_kinesis_stream.test_stream terraform-kinesis-test
```
