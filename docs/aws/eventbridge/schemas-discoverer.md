# Resource: aws_schemas_discoverer

Provides an EventBridge Schema Discoverer resource.

## Basic Example

```yaml
resource:
  aws_cloudwatch_event_bus:
    messenger:
      name: chat-messages

  aws_schemas_discoverer:
    test:
      source_arn: ${aws_cloudwatch_event_bus.messenger.arn}
      description: Auto discover event schemas```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `source_arn` - (Required) The ARN of the event bus to discover event schemas on.
* `description` - (Optional) The description of the discoverer. Maximum of 256 characters.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The Amazon Resource Name (ARN) of the discoverer.
* `id` - The ID of the discoverer.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_schemas_discoverer.test 123
```
