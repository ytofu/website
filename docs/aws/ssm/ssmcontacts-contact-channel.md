# Ssmcontacts Contact Channel

Manage Ssmcontacts Contact Channel resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ssmcontacts_contact_channel:
    example:
      contact_id: "arn:aws:ssm-contacts:us-west-2:123456789012:contact/contactalias"
      delivery_address:
        simple_address: email@example.com
      name: Example contact channel
      type: EMAIL
```

## Usage with SSM Contact

```yaml
resource:
  aws_ssmcontacts_contact:
    example_contact:
      alias: example_contact
      type: PERSONAL

resource:
  aws_ssmcontacts_contact_channel:
    example:
      contact_id: ${aws_ssmcontacts_contact.example_contact.arn}
      delivery_address:
        simple_address: email@example.com
      name: Example contact channel
      type: EMAIL
```
