# Sesv2 Contact List

Manage Sesv2 Contact List resources using ytofu YAML.

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
