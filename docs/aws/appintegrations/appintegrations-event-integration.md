# Resource: aws_appintegrations_event_integration

Provides an Amazon AppIntegrations Event Integration resource.

## Basic Example

```yaml
resource:
  aws_appintegrations_event_integration:
    example:
      name: example-name
      description: Example Description
      eventbridge_bus: default
      event_filter:
        source: aws.partner/examplepartner.com
      tags: 
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) Description of the Event Integration.
* `eventbridge_bus` - (Required) EventBridge bus.
* `event_filter` - (Required) Block that defines the configuration information for the event filter. The Event Filter block is documented below.
* `name` - (Required) Name of the Event Integration.
* `tags` - (Optional) Tags to apply to the Event Integration. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

A `event_filter` block supports the following arguments:

* `source` - (Required) Source of the events.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Event Integration.
* `id` - Identifier of the Event Integration which is the name of the Event Integration.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_appintegrations_event_integration.example example-name
```
