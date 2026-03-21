# Resource: aws_pinpointsmsvoicev2_configuration_set

Manages an AWS End User Messaging SMS Configuration Set.

## Basic Example

```yaml
resource:
  aws_pinpointsmsvoicev2_configuration_set:
    example:
      name: example-configuration-set
      default_sender_id: example
      default_message_type: TRANSACTIONAL
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the configuration set.
* `default_sender_id` - (Optional) The default sender ID to use for this configuration set.
* `default_message_type` - (Optional) The default message type. Must either be "TRANSACTIONAL" or "PROMOTIONAL"
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the configuration set.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_pinpointsmsvoicev2_configuration_set.example example-configuration-set
```
