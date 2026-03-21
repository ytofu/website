# Resource: aws_media_package_channel

Provides an AWS Elemental MediaPackage Channel.

## Basic Example

```yaml
resource:
  aws_media_package_channel:
    kittens:
      channel_id: kitten-channel
      description: A channel dedicated to amusing videos of kittens.
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `channel_id` - (Required) A unique identifier describing the channel
* `description` - (Optional) A description of the channel
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The same as `channel_id`
* `arn` - The ARN of the channel
* `hls_ingest` - A single item list of HLS ingest information
    * `ingest_endpoints` - A list of the ingest endpoints
        * `password` - The password
        * `url` - The URL
        * `username` - The username
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_media_package_channel.kittens kittens-channel
```
