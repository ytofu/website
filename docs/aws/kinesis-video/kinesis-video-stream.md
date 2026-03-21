# Resource: aws_kinesis_video_stream

Provides a Kinesis Video Stream resource. Amazon Kinesis Video Streams makes it easy to securely stream video from connected devices to AWS for analytics, machine learning (ML), playback, and other processing.

## Basic Example

```yaml
resource:
  aws_kinesis_video_stream:
    default:
      name: terraform-kinesis-video-stream
      data_retention_in_hours: 1
      device_name: kinesis-video-device-name
      media_type: video/h264
      tags:
        Name: terraform-kinesis-video-stream
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) A name to identify the stream. This is unique to the
AWS account and region the Stream is created in.
* `data_retention_in_hours` - (Optional) The number of hours that you want to retain the data in the stream. Kinesis Video Streams retains the data in a data store that is associated with the stream. The default value is `0`, indicating that the stream does not persist data.
* `device_name` - (Optional) The name of the device that is writing to the stream. **In the current implementation, Kinesis Video Streams does not use this name.**
* `kms_key_id` - (Optional) The ID of the AWS Key Management Service (AWS KMS) key that you want Kinesis Video Streams to use to encrypt stream data. If no key ID is specified, the default, Kinesis Video-managed key (`aws/kinesisvideo`) is used.
* `media_type` - (Optional) The media type of the stream. Consumers of the stream can use this information when processing the stream. For more information about media types, see [Media Types][2]. If you choose to specify the MediaType, see [Naming Requirements][3] for guidelines.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The unique Stream id
* `arn` - The Amazon Resource Name (ARN) specifying the Stream (same as `id`)
* `creation_time` - A time stamp that indicates when the stream was created.
* `version` - The version of the stream.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

- `create` - (Default `5m`)
- `update` - (Default `120m`)
- `delete` - (Default `120m`)

## Import

```bash
ytofu import aws_kinesis_video_stream.test_stream arn:aws:kinesisvideo:us-west-2:123456789012:stream/terraform-kinesis-test/1554978910975
```
