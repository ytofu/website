# Resource: aws_media_packagev2_channel_group

Creates an AWS Elemental MediaPackage Version 2 Channel Group.

## Basic Example

```yaml
resource:
  aws_media_packagev2_channel_group:
    example:
      name: example
      description: channel group for example channels
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) A unique identifier naming the channel group
* `description` - (Optional) A description of the channel group
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The ARN of the channel
* `description` - The same as `description`
* `egress_domain` - The egress domain of the channel group
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_media_packagev2_channel_group.example example
```
