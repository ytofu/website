# Resource: aws_ssmcontacts_contact_channel

ytofu resource for managing an AWS SSM Contacts Contact Channel.

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

## Argument Reference

This resource supports the following arguments:

- `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
- `contact_id` - (Required) Amazon Resource Name (ARN) of the AWS SSM Contact that the contact channel belongs to.
- `delivery_address` - (Required) Block that contains contact engagement details. See details below.
- `name` - (Required) Name of the contact channel. Must be between 1 and 255 characters, and may contain alphanumerics, underscores (`_`), hyphens (`-`), periods (`.`), and spaces.
- `type` - (Required) Type of the contact channel. One of `SMS`, `VOICE` or `EMAIL`.

### delivery_address

- `simple_address` - (Required) Details to engage this contact channel. The expected format depends on the contact channel type and is described in the [`ContactChannelAddress` section of the SSM Contacts API Reference](https://docs.aws.amazon.com/incident-manager/latest/APIReference/API_SSMContacts_ContactChannelAddress.html).

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

- `activation_status` - Whether the contact channel is activated. The contact channel must be activated to use it to engage the contact. One of `ACTIVATED` or `NOT_ACTIVATED`.
- `arn` - Amazon Resource Name (ARN) of the contact channel.

## Import

```bash
ytofu import aws_ssmcontacts_contact_channel.example arn:aws:ssm-contacts:us-west-2:123456789012:contact-channel/example
```
