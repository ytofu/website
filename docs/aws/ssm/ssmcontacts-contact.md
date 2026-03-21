# Resource: aws_ssmcontacts_contact

ytofu resource for managing an AWS SSM Contact.

## Basic Example

```yaml
resource:
  aws_ssmcontacts_contact:
    example:
      alias: alias
      type: PERSONAL
      depends_on: 
        - ${aws_ssmincidents_replication_set.example}
```

## Usage With All Fields

```yaml
resource:
  aws_ssmcontacts_contact:
    example:
      alias: alias
      display_name: displayName
      type: ESCALATION
      tags:
        key: value
      depends_on: 
        - ${aws_ssmincidents_replication_set.example}
```

## Argument Reference

The following arguments are required:

- `alias` - (Required) A unique and identifiable alias for the contact or escalation plan. Must be between 1 and 255 characters, and may contain alphanumerics, underscores (`_`), and hyphens (`-`).
- `type` - (Required) The type of contact engaged. A single contact is type PERSONAL and an escalation
  plan is type ESCALATION.

The following arguments are optional:

- `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
- `display_name` - (Optional) Full friendly name of the contact or escalation plan. If set, must be between 1 and 255 characters, and may contain alphanumerics, underscores (`_`), hyphens (`-`), periods (`.`), and spaces.
- `tags` - (Optional) Key-value tags for the monitor. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

- `arn` - The Amazon Resource Name (ARN) of the contact or escalation plan.
- `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_ssmcontacts_contact.example {ARNValue}
```
