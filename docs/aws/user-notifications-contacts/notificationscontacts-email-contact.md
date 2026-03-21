# Resource: aws_notificationscontacts_email_contact

ytofu resource for managing AWS User Notifications Contacts Email Contact.

## Basic Example

```yaml
resource:
  aws_notificationscontacts_email_contact:
    example:
      name: example-contact
      email_address: example@example.com
      tags:
        Environment: Production
```

## Argument Reference

The following arguments are required:

* `email_address` - (Required) Email address for the contact. Must be between 6 and 254 characters and match an email
  pattern.
* `name` - (Required) Name of the email contact. Must be between 1 and 64 characters and can contain alphanumeric
  characters, underscores, tildes, periods, and hyphens.

The following arguments are optional:

* `tags` - (Optional) Map of tags to assign to the resource. If configured with a provider 
  `default_tags` configuration block
  present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Email Contact.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider 
  `default_tags` configuration block.

## Import

```bash
ytofu import aws_notificationscontacts_email_contact.example arn:aws:notificationscontacts:us-west-2:123456789012:emailcontact:example-contact
```
