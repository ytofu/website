# Resource: aws_sesv2_contact_list

ytofu resource for managing an AWS SESv2 (Simple Email V2) Contact List.

## Basic Example

```yaml
resource:
  aws_sesv2_contact_list:
    example:
      contact_list_name: example
```

## Extended Usage

```yaml
resource:
  aws_sesv2_contact_list:
    example:
      contact_list_name: example
      description: description
      topic:
        default_subscription_status: OPT_IN
        description: topic description
        display_name: Example Topic
        topic_name: example-topic
```

## Argument Reference

The following arguments are required:

* `contact_list_name` - (Required) Name of the contact list.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) Description of what the contact list is about.
* `tags` - (Optional) Key-value map of resource tags for the contact list. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `topic` - (Optional) Configuration block(s) with topic for the contact list. Detailed below.

### topic

The following arguments are required:

* `default_subscription_status` - (Required) Default subscription status to be applied to a contact if the contact has not noted their preference for subscribing to a topic.
* `display_name` - (Required) Name of the topic the contact will see.
* `topic_name` - (Required) Name of the topic.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) Description of what the topic is about, which the contact will see.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `created_timestamp` - Timestamp noting when the contact list was created in ISO 8601 format.
* `id` - Name of the contact list.
* `last_updated_timestamp` - Timestamp noting the last time the contact list was updated in ISO 8601 format.

## Import

```bash
ytofu import aws_sesv2_contact_list.example example
```
